---
title: Dstat-Tools
layout: post
categories: Ruby dstat gnuplot
---

A dstat monitor plotting script for data from multiple nodes of a cluster.

This ruby script uses GNUPlot through a ruby wrapper [(ruby_gnuplot)](https://github.com/rdp/ruby_gnuplot/blob/master/README.textile) to plot csv data generated by mvneves' [dstat-monitor](https://github.com/mvneves/dstat-monitor).

### Pre-requisites and Installation

You need an installation of the ruby programming language, X11, GNUPlot and the ruby_gnuplot gem. The gems csv and optparse are part of the ruby standard library.

To install on a Mac do the following steps:
```
1. Install XQuartz from here:
    http://xquartz.macosforge.org/landing/
2. Install gnuplot with homebrew:
    brew install gnuplot --with-x11
3. Install gnuplot gem:
    gem install gnuplot
```

For linux the procedure is
```
1. Install gnuplot (your distribution might come with it though)
    sudo apt-get install gnuplot
2. Install gnuplot gem:
    gem install gnuplot
3. Install csv gem
    gem install fastercsv
```

### Usage

```
Usage:
dstat_plot.rb [options] -c CATEGORY -f FIELD [directory | file1 file2 ...] or
dstat_plot.rb [options] -l COLUMN [directory | file1 file2 ...]
    -v, --verbose                    Output more information
    -i, --invert [VALUE]             Invert the graph such that inverted(x) = VALUE - f(x),
                                     default is 100.
    -n, --no-key                     No plot key is printed.
    -d, --dry                        Dry run. Plot is not saved to file but instead displayed with gnuplot.
    -o, --output FILE|DIR            File or Directory that plot should be saved to.
                                     If a directory is given the filename will be generated.
                                     Default is csv file directory.
    -y, --y-range RANGE              Sets the y-axis range. Default is 105. If a value exceeds
                                     this range, "autoscale" is enabled.
    -t, --title TITLE                Override the default title of the plot.
    -s, --smoothing ALGORITHM        Smooths the graph using the given algorithm.
    -a, --average-over SLICE_SIZE    Calculates the average for slice_size large groups of values.

    -c, --category CATEGORY          Select the category.
    -f, --field FIELD                Select the field.
    -l, --column COLUMN              Select the desired column directly.
    
    -h, --help                       Display this screen.
```

(-c CATEGORY -f FIELD or -l COLUMN are mandatory parameters)

The plot is saved as category-field.png in the folder where the csv files are located unless -o PATH explicitly specifies a different destination.

### Example

```
ruby dstat_plot.rb -c "total cpu usage" -f "usr" example.csv
```
![example plot](http://i.imgur.com/Gfo5rfH.png)

The equivalent with the -l option would be

```
ruby dstat_plot.rb -l 11 example.csv
```
### Possible category - field combinations

(N is the cpu core index for 0..n cores)

Categoriy | Field | Column | Categoriy | Field | Column |
----------|-------|--------|-----------|-------|--------|
epoch     | epoch |  0 | net/total | recv | 23 |
memory usage | used | 1 |           | send | 24 |
          | buff  |  2 | net/eth0  | recv | 25 |
          | cach  |  3 |           | send | 26 |
          | free  |  4 | dsk/total | read | 27 |
swap      | used  |  5 |           | writ | 28 |
          |free   |  6 | dsk/sda   | read | 29 |
system    | int   |  7 |           | writ | 30 |
          |csv    |  8 | io/total  | read | 31 |
paging    | in    |  9 |           | writ | 32 |
          |out    |  10 | io/sda    | read | 33 |
total cpu usage   | usr | 11 |       | writ | 34 |
          | sys | 12 |
          | idl | 13 |
          | wai | 14 |
          | hiq | 15 |
          | siq | 16 |
cpuN usage | usr | 17 |
          | sys | 18 |
          | idl | 19 |
          | wai | 20 |
          | hiq | 21 |
          | siq | 22 |


### Smoothing

You can take advantage of a variety of different smoothing algorithms to make your plots more easy on the eye, especially if you're plotting data from a large number of nodes all in one plot.

To do so use the options --smoothing ALGORITHM when running dstat-plot

Available smoothing algorithms are
```
unique, frequency, cumulative, cnormal, kdensity, unwrap, csplines, acsplines, mcsplines, bezier, sbezier
```

As an example
```
ruby dstat_plot.rb -s acsplines -c "total cpu usage" -f "usr" example.csv
```

will give you the following result
![smoothing example](http://i.imgur.com/BE1egf2.png)