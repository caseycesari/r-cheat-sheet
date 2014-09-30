##R Cheat Sheet

Turn off scientific notation except for very large numbers

	options(scipen=20)

[source](http://stackoverflow.com/questions/5352099/how-to-disable-scientific-notation-in-r)

###Data transformation

Make a new date column from a column with datetime data stored as a string

	data$date <- as.POSIXct(data$date, format='%m/%d/%Y')

or

	data$date <- as.Date(data$date, format="%m/%d/%y")

[source](http://stackoverflow.com/questions/10128529/creating-a-new-column-for-date-info-with-specific-date-format)
[source](http://stackoverflow.com/questions/14471640/r-subset-by-date)

Convert a column containing a string of UNIX time to a date

	date[, {column number}] <- as.Date(as.POSIXct(data[, {column number}], origin='1970-01-01'))

Group and sum a column into a new dataframe
					
	# Assuming a following data frame structured as data[store, revenue, date]

	new <- aggregate(data$revenue, by=list(date=data$date), FUN=sum)

[source](http://stackoverflow.com/questions/1660124/how-to-group-columns-by-sum-in-r)

Subset a dataframe by a date range

	subset <- subset(data, date >= '2000-01-01' & date <= '2010-01-01')
	
[source](http://stackoverflow.com/questions/17708805/subset-data-frame-for-specific-dates)

Subset a dataframe by regex matching

	subset <- subset(data, grepl("regex", data[[column number]]))

[source](http://stackoverflow.com/questions/2125231/subsetting-in-r-using-or-condition-with-strings)

Rename dataframe column names

	colnames(date) <- c("column 1 name", "column 2 name", "column 3 name")

[source](http://stackoverflow.com/questions/6081439/changing-column-names-of-a-data-frame-in-r)

Sort a dataframe

	attach(data)
	sorted <- data[order(sort_column) , ] 
	# or, in decending order
	sorted <- data[order(-sort_column) , ]
	detach(data)

[source](http://www.ats.ucla.edu/stat/r/faq/sort.htm)

###Analysis

Generate a table of frequencies for the values in a single column

	count_of_value <- as.data.frame(table(data["column"]))
	
[source](http://stackoverflow.com/questions/11148868/how-to-generate-a-frequency-table-in-r)

###Graphing

Make a timeseries line chart by group
	
	# Assuming a following data frame structured as data[store, revenue, date]
	# and library("ggplot2")

	qplot(date, revenue, data=data, group=store, geom="line")

[source](http://docs.ggplot2.org/current/geom_line.html)

Turn off axes, and add your own customized verions

	plot(data, axes=FALSE)

	# See ?axis for options
	axis(...)

[source](http://stackoverflow.com/questions/11019870/changing-y-axis-tick-labels-from-standard-form-to-the-full-number)

###Mapping

Amanda Cox's [R Training](https://gist.github.com/ashaw/94072018b242cf0605dd) from #NICAR13
