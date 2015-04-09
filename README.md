# udqct
The Untitled Data Quality Check Tool

## Overview

The purpose of this is to be able to quickly find Points of Concern in spreadsheets of data. It's to let you know about outliers and missing data *before* you get all excited about that regression you ran (but haven't looked a the scatterplot).

It should show the *type* of data you have: show whether it is *identifying* (unique or nearly so), *categorical* (eg, group assignment), *continuous* (can take many values), *ordinal* (ordered, but not so many values), or *missing.*

*We'll need heuristics for detecting these. Do we need to differentiate between Ordinal and Continuous in this tool?*

Target data size is in the 300 rows by 1000 columns neighborhood. *What do we do with data much larger than this?*

Basic layout will probably be a grid, with cells colored by data type. Continuous (and ordinal?) columns are be colored with a diverging color ramp corresponding to the demeaned, z-scored value. Most values will be very close to the center of this scale; outliers will get a big jump to the extreme ends. *Or maybe there won't be a color ramp for non-outlier points? Do we care about how that distribution looks by color? Will people be tempted to see non-useful patterns? If you can sort, this might be more useful.*

Categorical data will get colors (from the same family) for each value, to show general variability. *Or maybe no ramp for categorical points, either; just the same color?*

Identifying data will be shown in a single (muted) color.

Missing data will be shown in a single (distinct) color.

ANYHOW essentially color will be how you tell if a cell is *identifying,* *normal,* *outlying,* or *missing.* I think that's the essential distinction. Indicating low/high outlying points may be important, too.

## What Can You Do?

You can *navigate* -- you need to be able to somehow see what you have in a substantially large data file. Probably, trying to stuff everything into one viewport won't work very well.

You can *filter* -- show only columns/rows with outlying points, also filter rows or columns with some kind of search.

You can *query* -- how many outliers are in this row? What is the distribution of values in this column? Is it significantly non-normal? What is the value of this cell and where is it on the column's overall distribution?

You can *censor* -- if I leave a cell's value out, how does the column's distribution change? Mainly, this will be to alleviate scaling problems in viweing the distribution.

## What *Can't* You Do?

You can't change values.

You can't impute values.

You can't annotate things, or keep any particular state. This is not a lab notebook.

You (probably?) can't download the data.

You can't download a picture of the data.

## Implementation

Backend is (probably) python+flask+pandas+pytables. Frontend is HTML5. Render in maybe HTML table, maybe canvas or webgl if necessary.