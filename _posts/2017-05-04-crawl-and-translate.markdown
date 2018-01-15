---
title: Crawl and Translate with Google
layout: post
tags: ruby
---

Something that I've been meaning to do for quite some time finally happened: I wrote a little, very specific crawler to get some text off of a website and then immediately translated the result using the very convenient google-translate sdk.

I did it to help my father with some research and it's not 100% refactored but it was quite some fun to play around with.

This is the crawler that looks for specific fields on a number of websites, the URLs of which are saves in a simple textfile. the result is written to a csv file.

{% highlight ruby %}
require 'nokogiri'
require 'open-uri'
require 'csv'

urls = File.readlines('pages.txt').map(&:chomp)

lines = urls.map do |url|
  begin
    page = Nokogiri::HTML(open(url).read, nil , 'utf-8')

    project_id = page.css('div.top').css('div.left').css('div.id').text.strip
    project_title = page.css('div.top').css('div.left').css('h1')[0].text.strip
    project_description = page.css('div.top').css('div.left').css('p')[0].text.delete("\r\n")

    details = page.css('div.grid.introduction').css('div.left').css('div')
    section_titles = details.css('h3').map(&:text)
    section_texts = details.css('p').map{ |element| element.text.chop.chomp }
    sections = section_titles.zip(section_texts).map { |section| { title: section[0].chomp, text: section[1]} }

    line = [project_id, project_title, project_description]
    sections.each do |section|
      line << section[:title]
      line << section[:text]
    end

    line
  rescue OpenURI::HTTPError
    puts "URL #{url} appears to be invalid."
  end
end

CSV.open("content-2.csv", "wb") do |csv|
  lines.each { |line| csv << line }
end

{% endhighlight %}

The translation script takes the csv as input and simply invokes the google translate api and writes back the results. Fast simple and efficient.

```ruby
require 'google/cloud/translate'
require 'csv'

project_id = "***"
translate = Google::Cloud::Translate.new project: project_id, key: "***"

origin = "en"
target = "de"

csv = CSV.read('content-2.csv')

csv_translated = csv.map do |row|
  row.map do |item|
    translate.translate item, from: origin, to: target
  end
end

CSV.open("translation.csv", "wb") do |csv|
  csv_translated.each { |line| csv << line }
end
```
