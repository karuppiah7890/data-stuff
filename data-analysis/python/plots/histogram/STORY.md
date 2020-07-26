# histogram

I'm following this blog post

https://towardsdatascience.com/histograms-and-density-plots-in-python-f6bda88f5ac0

To draw the histogram plot, I need some data first. I could get any data
or create my own data. But I liked the example in the blog post. It's a real
world example, about NYC flights. So, I'm trying to get the data set - the csv.
And it's turning out to be harder than I thought.

---

I need to get the data from this R package - 
https://cran.r-project.org/web/packages/nycflights13/index.html

Source code of it is here - https://github.com/hadley/nycflights13

I think I need to install the package and get the data from it? And dump or
export the data as a CSV

I'm installing R from here for Mac OS X
https://cran.r-project.org/bin/macosx/

This shows how to install packages and load and unload them -

https://www.dummies.com/programming/r/how-to-install-load-and-unload-packages-in-r/

I finally installed R programming language in my system. It took forever to
download for some reason. I think the servers were slow, as pip install and
stuff worked just fine during the same time

```bash
$ r
> install.packages('nycflights13')
```

Got some weird error

```bash
The downloaded binary packages are in
        /var/folders/fg/55xcrj215gs2n9gnpz4077y40000gq/T//Rtmpp44h7W/downloaded_packages
Warning message:
In doTryCatch(return(expr), name, parentenv, handler) :
  unable to load shared object '/Library/Frameworks/R.framework/Resources/modules//R_X11.so':
  dlopen(/Library/Frameworks/R.framework/Resources/modules//R_X11.so, 6): Library not loaded: /opt/X11/lib/libSM.6.dylib
  Referenced from: /Library/Frameworks/R.framework/Versions/4.0/Resources/modules/R_X11.so
  Reason: image not found
```

As mentioned in https://cran.r-project.org/bin/macosx/ , I had to reinstall
XQaurtz, which is also mentioned here - https://stackoverflow.com/questions/26489928/cant-load-x11-in-r-after-os-x-yosemite-upgrade#26797061 , which I found on
searching the error I got.

And I was fool to keep trying `load()` instead of `library()` to load the
library. Anyways, this is what finally worked

```bash
> library('nycflights13')
> flights
# A tibble: 336,776 x 19
    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
 1  2013     1     1      517            515         2      830            819
 2  2013     1     1      533            529         4      850            830
 3  2013     1     1      542            540         2      923            850
 4  2013     1     1      544            545        -1     1004           1022
 5  2013     1     1      554            600        -6      812            837
 6  2013     1     1      554            558        -4      740            728
 7  2013     1     1      555            600        -5      913            854
 8  2013     1     1      557            600        -3      709            723
 9  2013     1     1      557            600        -3      838            846
10  2013     1     1      558            600        -2      753            745
# … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
#   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
#   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>
```

Found out how to export data - https://datatofish.com/export-dataframe-to-csv-in-r/ .
So I can export my dataframe to a csv :)

```bash
> write.csv(flights, "/Users/karuppiahn/oss/github.com/karuppiah7890/data-stuff/data-analysis/python/plots/histogram/flights.csv", row.names = TRUE)
```

---

Now I'm back to writing some python code! And trying out histograms! :)

I got the python VS Code extension and it also prompted me to install
pylint for linting. I made sure it's enabled only in the current workspace
that I'm working in, and is generally disabled. Too many global plugins,
unnecessary ones, are crazy! 😅

I started writing some basic code in python. Like importing pandas and then
reading the csv file. But then when I ran it using `python simple_histogram.py`,
it just didn't show anything. Then I had to use `print()` statement. I realized
that there's some cool features in jupyter notebooks that's helping. Like,
it can put code and instructions or text together, yes, and it can also
just show the output of the last line of code and it can show visualizations.
I don't know how it will workout in the command line. I need to check it out.
For now, I'm just getting jupyter notebook in my local, though there's Google
Colab, the online version.

https://jupyter.org/
https://jupyter.org/install.html

I noticed there's something called jupyter lab, and jupyter notebook. Looks like
jupyter lab is a superset of jupyter notebook which contains a bit more. So
I just got the jupyter lab

```bash
$ pip install jupyterlab
$ jupyterlab
```

That opened up the web app jupyter lab and it showed the files I had in the
directory where I ran the command! So now I have access to the big CSV file -
35 MB or so! Thinking if I should check it in or not. Checking it in would
be too much I think 😅 I could checkin a part of it. Hmm. I'll think about it!
May be I could push it for now? And then get rid of it later? But it will still
be there in my git history. That will be a lot!

For now I ignored the csv file in `.gitignore` and also the `.ipynb_checkpoints`
directory at the project root to make sure no sub directory or project
directory has it. I think it's some sort of git like thingy. Confirmed that
they are usually ignored in git over here - https://www.toptal.com/developers/gitignore/api/jupyternotebooks



---

Learnings:
* Histograms are a great way to get started with exploring a single variable


