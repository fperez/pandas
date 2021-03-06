=============
Release Notes
=============

This is the list of changes to pandas between each release. For full details,
see the commit logs at http://github.com/wesm/pandas

What is it
----------

pandas is a Python package providing fast, flexible, and expressive data
structures designed to make working with “relational” or “labeled” data both
easy and intuitive. It aims to be the fundamental high-level building block for
doing practical, real world data analysis in Python. Additionally, it has the
broader goal of becoming the most powerful and flexible open source data
analysis / manipulation tool available in any language.

Where to get it
---------------

* Source code: http://github.com/wesm/pandas
* Binary installers on PyPI: http://pypi.python.org/pypi/pandas
* Documentation: http://pandas.sourceforge.net

pandas 0.6.1
============

**Release date:** Not yet released

**New features / modules**

  - Can pass Series to DataFrame.append with ignore_index=True for appending a
    single row (GH #430)
  - Add Spearman and Kendall correlation options to Series.corr and
    DataFrame.corr (GH #428)

**Improvements to existing features**
  - Improve memory usage of `DataFrame.describe` (do not copy data
    unnecessarily) (PR #425)
  - Use same formatting function for outputting floating point Series to console
    as in DataFrame (PR #420)
  - DataFrame.delevel will try to infer better dtype for new columns (GH #440)
  - Exclude non-numeric types in DataFrame.{corr, cov}
  - Override Index.astype to enable dtype casting (GH #412)

**Bug fixes**

  - `DataFrame.count` should return Series with zero instead of NA with length-0
    axis (GH #423)
  - Fix Yahoo! Finance API usage in pandas.io.data (GH #419, PR #427)
  - Fix upstream bug causing failure in Series.align with empty Series (GH #434)
  - Function passed to DataFrame.apply can return a list, as long as it's the
    right length. Regression from 0.4 (GH #432)
  - Don't "accidentally" upcast scalar values when indexing using .ix (GH #431)
  - Fix groupby exception raised with as_index=False and single column selected
    (GH #421)

Thanks
------
- Ralph Bean
- Wouter Overmeire
- Joon Ro
- Chang She
- Chris Uga

pandas 0.6.0
============

**Release date:** 11/25/2011

**API Changes**

  - Arithmetic methods like `sum` will attempt to sum dtype=object values by
    default instead of excluding them (GH #382)

**New features / modules**

  - Add `melt` function to `pandas.core.reshape`
  - Add `level` parameter to group by level in Series and DataFrame
    descriptive statistics (PR #313)
  - Add `head` and `tail` methods to Series, analogous to to DataFrame (PR
    #296)
  - Add `Series.isin` function which checks if each value is contained in a
    passed sequence (GH #289)
  - Add `float_format` option to `Series.to_string`
  - Add `skip_footer` (GH #291) and `converters` (GH #343) options to
    `read_csv` and `read_table`
  - Add proper, tested weighted least squares to standard and panel OLS (GH
    #303)
  - Add `drop_duplicates` and `duplicated` functions for removing duplicate
    DataFrame rows and checking for duplicate rows, respectively (GH #319)
  - Implement logical (boolean) operators &, |, ^ on DataFrame (GH #347)
  - Add `Series.mad`, mean absolute deviation, matching DataFrame
  - Add `QuarterEnd` DateOffset (PR #321)
  - Add matrix multiplication function `dot` to DataFrame (GH #65)
  - Add `orient` option to `Panel.from_dict` to ease creation of mixed-type
    Panels (GH #359, #301)
  - Add `DataFrame.from_dict` with similar `orient` option
  - Can now pass list of tuples or list of lists to `DataFrame.from_records`
    for fast conversion to DataFrame (GH #357)
  - Can pass multiple levels to groupby, e.g. `df.groupby(level=[0, 1])` (GH
    #103)
  - Can sort by multiple columns in `DataFrame.sort_index` (GH #92, PR #362)
  - Add fast `get_value` and `put_value` methods to DataFrame and
    micro-performance tweaks (GH #360)
  - Add `cov` instance methods to Series and DataFrame (GH #194, PR #362)
  - Add bar plot option to `DataFrame.plot` (PR #348)
  - Add `idxmin` and `idxmax` functions to Series and DataFrame for computing
    index labels achieving maximum and minimum values (PR #286)
  - Add `read_clipboard` function for parsing DataFrame from OS clipboard,
    should work across platforms (GH #300)
  - Add `nunique` function to Series for counting unique elements (GH #297)
  - DataFrame constructor will use Series name if no columns passed (GH #373)
  - Support regular expressions and longer delimiters in read_table/read_csv,
    but does not handle quoted strings yet (GH #364)
  - Add `DataFrame.to_html` for formatting DataFrame to HTML (PR #387)
  - MaskedArray can be passed to DataFrame constructor and masked values will be
    converted to NaN (PR #396)
  - Add `DataFrame.boxplot` function (GH #368, others)
  - Can pass extra args, kwds to DataFrame.apply (GH #376)

**Improvements to existing features**

  - Raise more helpful exception if date parsing fails in DateRange (GH #298)
  - Vastly improved performance of GroupBy on axes with a MultiIndex (GH #299)
  - Print level names in hierarchical index in Series repr (GH #305)
  - Return DataFrame when performing GroupBy on selected column and
    as_index=False (GH #308)
  - Can pass vector to `on` argument in `DataFrame.join` (GH #312)
  - Don't show Series name if it's None in the repr, also omit length for short
    Series (GH #317)
  - Show legend by default in `DataFrame.plot`, add `legend` boolean flag (GH
    #324)
  - Significantly improved performance of `Series.order`, which also makes
    np.unique called on a Series faster (GH #327)
  - Faster cythonized count by level in Series and DataFrame (GH #341)
  - Raise exception if dateutil 2.0 installed on Python 2.x runtime (GH #346)
  - Significant GroupBy performance enhancement with multiple keys with many
    "empty" combinations
  - New Cython vectorized function `map_infer` speeds up `Series.apply` and
    `Series.map` significantly when passed elementwise Python function,
    motivated by PR #355
  - Cythonized `cache_readonly`, resulting in substantial micro-performance
    enhancements throughout the codebase (GH #361)
  - Special Cython matrix iterator for applying arbitrary reduction operations
    with 3-5x better performance than `np.apply_along_axis` (GH #309)
  - Add `raw` option to `DataFrame.apply` for getting better performance when
    the passed function only requires an ndarray (GH #309)
  - Improve performance of `MultiIndex.from_tuples`
  - Can pass multiple levels to `stack` and `unstack` (GH #370)
  - Can pass multiple values columns to `pivot_table` (GH #381)
  - Can call `DataFrame.delevel` with standard Index with name set (GH #393)
  - Use Series name in GroupBy for result index (GH #363)
  - Refactor Series/DataFrame stat methods to use common set of NaN-friendly
    function
  - Handle NumPy scalar integers at C level in Cython conversion routines

**Bug fixes**

  - Fix bug in `DataFrame.to_csv` when writing a DataFrame with an index
    name (GH #290)
  - DataFrame should clear its Series caches on consolidation, was causing
    "stale" Series to be returned in some corner cases (GH #304)
  - DataFrame constructor failed if a column had a list of tuples (GH #293)
  - Ensure that `Series.apply` always returns a Series and implement
    `Series.round` (GH #314)
  - Support boolean columns in Cythonized groupby functions (GH #315)
  - `DataFrame.describe` should not fail if there are no numeric columns,
    instead return categorical describe (GH #323)
  - Fixed bug which could cause columns to be printed in wrong order in
    `DataFrame.to_string` if specific list of columns passed (GH #325)
  - Fix legend plotting failure if DataFrame columns are integers (GH #326)
  - Shift start date back by one month for Yahoo! Finance API in pandas.io.data
    (GH #329)
  - Fix `DataFrame.join` failure on unconsolidated inputs (GH #331)
  - DataFrame.min/max will no longer fail on mixed-type DataFrame (GH #337)
  - Fix `read_csv` / `read_table` failure when passing list to index_col that is
    not in ascending order (GH #349)
  - Fix failure passing Int64Index to Index.union when both are monotonic
  - Fix error when passing SparseSeries to (dense) DataFrame constructor
  - Added missing bang at top of setup.py (GH #352)
  - Change `is_monotonic` on MultiIndex so it properly compares the tuples
  - Fix MultiIndex outer join logic (GH #351)
  - Set index name attribute with single-key groupby (GH #358)
  - Bug fix in reflexive binary addition in Series and DataFrame for
    non-commutative operations (like string concatenation) (GH #353)
  - setupegg.py will invoke Cython (GH #192)
  - Fix block consolidation bug after inserting column into MultiIndex (GH #366)
  - Fix bug in join operations between Index and Int64Index (GH #367)
  - Handle min_periods=0 case in moving window functions (GH #365)
  - Fixed corner cases in DataFrame.apply/pivot with empty DataFrame (GH #378)
  - Fixed repr exception when Series name is a tuple
  - Always return DateRange from `asfreq` (GH #390)
  - Pass level names to `swaplavel` (GH #379)
  - Don't lose index names in `MultiIndex.droplevel` (GH #394)
  - Infer more proper return type in `DataFrame.apply` when no columns or rows
    depending on whether the passed function is a reduction (GH #389)
  - Always return NA/NaN from Series.min/max and DataFrame.min/max when all of a
    row/column/values are NA (GH #384)
  - Enable partial setting with .ix / advanced indexing (GH #397)
  - Handle mixed-type DataFrames correctly in unstack, do not lose type
    information (GH #403)
  - Fix integer name formatting bug in Index.format and in Series.__repr__
  - Handle label types other than string passed to groupby (GH #405)
  - Fix bug in .ix-based indexing with partial retrieval when a label is not
    contained in a level
  - Index name was not being pickled (GH #408)
  - Level name should be passed to result index in GroupBy.apply (GH #416)

Thanks
------

- Craig Austin
- Marius Cobzarenco
- Joel Cross
- Jeff Hammerbacher
- Adam Klein
- Thomas Kluyver
- Jev Kuznetsov
- Kieran O'Mahony
- Wouter Overmeire
- Nathan Pinger
- Christian Prinoth
- Skipper Seabold
- Chang She
- Ted Square
- Aman Thakral
- Chris Uga
- Dieter Vandenbussche
- carljv
- rsamson

pandas 0.5.0
============

**Release date:** 10/24/2011

This release of pandas includes a number of API changes (see below) and cleanup
of deprecated APIs from pre-0.4.0 releases. There are also bug fixes, new
features, numerous significant performance enhancements, and includes a new
IPython completer hook to enable tab completion of DataFrame columns accesses
as attributes (a new feature).

In addition to the changes listed here from 0.4.3 to 0.5.0, the minor releases
0.4.1, 0.4.2, and 0.4.3 brought some significant new functionality and
performance improvements that are worth taking a look at.

Thanks to all for bug reports, contributed patches and generally providing
feedback on the library.

**API Changes**

  - `read_table`, `read_csv`, and `ExcelFile.parse` default arguments for
    `index_col` is now None. To use one or more of the columns as the resulting
    DataFrame's index, these must be explicitly specified now
  - Parsing functions like `read_csv` no longer parse dates by default (GH
    #225)
  - Removed `weights` option in panel regression which was not doing anything
    principled (GH #155)
  - Changed `buffer` argument name in `Series.to_string` to `buf`
  - `Series.to_string` and `DataFrame.to_string` now return strings by default
    instead of printing to sys.stdout
  - Deprecated `nanRep` argument in various `to_string` and `to_csv` functions
    in favor of `na_rep`. Will be removed in 0.6 (GH #275)
  - Renamed `delimiter` to `sep` in `DataFrame.from_csv` for consistency
  - Changed order of `Series.clip` arguments to match those of `numpy.clip` and
    added (unimplemented) `out` argument so `numpy.clip` can be called on a
    Series (GH #272)
  - Series functions renamed (and thus deprecated) in 0.4 series have been
    removed:

    * `asOf`, use `asof`
    * `toDict`, use `to_dict`
    * `toString`, use `to_string`
    * `toCSV`, use `to_csv`
    * `merge`, use `map`
    * `applymap`, use `apply`
    * `combineFirst`, use `combine_first`
    * `_firstTimeWithValue` use `first_valid_index`
    * `_lastTimeWithValue` use `last_valid_index`

  - DataFrame functions renamed / deprecated in 0.4 series have been removed:

    * `asMatrix` method, use `as_matrix` or `values` attribute
    * `combineFirst`, use `combine_first`
    * `getXS`, use `xs`
    * `merge`, use `join`
    * `fromRecords`, use `from_records`
    * `fromcsv`, use `from_csv`
    * `toRecords`, use `to_records`
    * `toDict`, use `to_dict`
    * `toString`, use `to_string`
    * `toCSV`, use `to_csv`
    * `_firstTimeWithValue` use `first_valid_index`
    * `_lastTimeWithValue` use `last_valid_index`
    * `toDataMatrix` is no longer needed
    * `rows()` method, use `index` attribute
    * `cols()` method, use `columns` attribute
    * `dropEmptyRows()`, use `dropna(how='all')`
    * `dropIncompleteRows()`, use `dropna()`
    * `tapply(f)`, use `apply(f, axis=1)`
    * `tgroupby(keyfunc, aggfunc)`, use `groupby` with `axis=1`

  - Other outstanding deprecations have been removed:

    * `indexField` argument in `DataFrame.from_records`
    * `missingAtEnd` argument in `Series.order`. Use `na_last` instead
    * `Series.fromValue` classmethod, use regular `Series` constructor instead
    * Functions `parseCSV`, `parseText`, and `parseExcel` methods in
      `pandas.io.parsers` have been removed
    * `Index.asOfDate` function
    * `Panel.getMinorXS` (use `minor_xs`) and `Panel.getMajorXS` (use
      `major_xs`)
    * `Panel.toWide`, use `Panel.to_wide` instead

**New features / modules**

  - Added `DataFrame.align` method with standard join options
  - Added `parse_dates` option to `read_csv` and `read_table` methods to
    optionally try to parse dates in the index columns
  - Add `nrows`, `chunksize`, and `iterator` arguments to `read_csv` and
    `read_table`. The last two return a new `TextParser` class capable of
    lazily iterating through chunks of a flat file (GH #242)
  - Added ability to join on multiple columns in `DataFrame.join` (GH #214)
  - Added private `_get_duplicates` function to `Index` for identifying
    duplicate values more easily
  - Added column attribute access to DataFrame, e.g. df.A equivalent to df['A']
    if 'A' is a column in the DataFrame (PR #213)
  - Added IPython tab completion hook for DataFrame columns. (PR #233, GH #230)
  - Implement `Series.describe` for Series containing objects (PR #241)
  - Add inner join option to `DataFrame.join` when joining on key(s) (GH #248)
  - Can select set of DataFrame columns by passing a list to `__getitem__` (GH
    #253)
  - Can use & and | to intersection / union Index objects, respectively (GH
    #261)
  - Added `pivot_table` convenience function to pandas namespace (GH #234)
  - Implemented `Panel.rename_axis` function (GH #243)
  - DataFrame will show index level names in console output
  - Implemented `Panel.take`
  - Add `set_eng_float_format` function for setting alternate DataFrame
    floating point string formatting
  - Add convenience `set_index` function for creating a DataFrame index from
    its existing columns

**Improvements to existing features**

  - Major performance improvements in file parsing functions `read_csv` and
    `read_table`
  - Added Cython function for converting tuples to ndarray very fast. Speeds up
    many MultiIndex-related operations
  - File parsing functions like `read_csv` and `read_table` will explicitly
    check if a parsed index has duplicates and raise a more helpful exception
    rather than deferring the check until later
  - Refactored merging / joining code into a tidy class and disabled unnecessary
    computations in the float/object case, thus getting about 10% better
    performance (GH #211)
  - Improved speed of `DataFrame.xs` on mixed-type DataFrame objects by about
    5x, regression from 0.3.0 (GH #215)
  - With new `DataFrame.align` method, speeding up binary operations between
    differently-indexed DataFrame objects by 10-25%.
  - Significantly sped up conversion of nested dict into DataFrame (GH #212)
  - Can pass hierarchical index level name to `groupby` instead of the level
    number if desired (GH #223)
  - Add support for different delimiters in `DataFrame.to_csv` (PR #244)
  - Add more helpful error message when importing pandas post-installation from
    the source directory (GH #250)
  - Significantly speed up DataFrame `__repr__` and `count` on large mixed-type
    DataFrame objects
  - Better handling of pyx file dependencies in Cython module build (GH #271)

**Bug fixes**

  - `read_csv` / `read_table` fixes
    - Be less aggressive about converting float->int in cases of floating point
      representations of integers like 1.0, 2.0, etc.
    - "True"/"False" will not get correctly converted to boolean
    - Index name attribute will get set when specifying an index column
    - Passing column names should force `header=None` (GH #257)
    - Don't modify passed column names when `index_col` is not
      None (GH #258)
    - Can sniff CSV separator in zip file (since seek is not supported, was
      failing before)
  - Worked around matplotlib "bug" in which series[:, np.newaxis] fails. Should
    be reported upstream to matplotlib (GH #224)
  - DataFrame.iteritems was not returning Series with the name attribute
    set. Also neither was DataFrame._series
  - Can store datetime.date objects in HDFStore (GH #231)
  - Index and Series names are now stored in HDFStore
  - Fixed problem in which data would get upcasted to object dtype in
    GroupBy.apply operations (GH #237)
  - Fixed outer join bug with empty DataFrame (GH #238)
  - Can create empty Panel (GH #239)
  - Fix join on single key when passing list with 1 entry (GH #246)
  - Don't raise Exception on plotting DataFrame with an all-NA column (GH #251,
    PR #254)
  - Bug min/max errors when called on integer DataFrames (PR #241)
  - `DataFrame.iteritems` and `DataFrame._series` not assigning name attribute
  - Panel.__repr__ raised exception on length-0 major/minor axes
  - `DataFrame.join` on key with empty DataFrame produced incorrect columns
  - Implemented `MultiIndex.diff` (GH #260)
  - `Int64Index.take` and `MultiIndex.take` lost name field, fix downstream
    issue GH #262
  - Can pass list of tuples to `Series` (GH #270)
  - Can pass level name to `DataFrame.stack`
  - Support set operations between MultiIndex and Index
  - Fix many corner cases in MultiIndex set operations
    - Fix MultiIndex-handling bug with GroupBy.apply when returned groups are not
    indexed the same
  - Fix corner case bugs in DataFrame.apply
  - Setting DataFrame index did not cause Series cache to get cleared
  - Various int32 -> int64 platform-specific issues
  - Don't be too aggressive converting to integer when parsing file with
    MultiIndex (GH #285)
  - Fix bug when slicing Series with negative indices before beginning

Thanks
------

- Thomas Kluyver
- Daniel Fortunov
- Aman Thakral
- Luca Beltrame
- Wouter Overmeire

pandas 0.4.3
============

Release notes
-------------

**Release date:** 10/9/2011

This is largely a bugfix release from 0.4.2 but also includes a handful of new
and enhanced features. Also, pandas can now be installed and used on Python 3
(thanks Thomas Kluyver!).

**New features / modules**

  - Python 3 support using 2to3 (PR #200, Thomas Kluyver)
  - Add `name` attribute to `Series` and added relevant logic and tests. Name
    now prints as part of `Series.__repr__`
  - Add `name` attribute to standard Index so that stacking / unstacking does
    not discard names and so that indexed DataFrame objects can be reliably
    round-tripped to flat files, pickle, HDF5, etc.
  - Add `isnull` and `notnull` as instance methods on Series (PR #209, GH #203)

**Improvements to existing features**

  - Skip xlrd-related unit tests if not installed
  - `Index.append` and `MultiIndex.append` can accept a list of Index objects to
    concatenate together
  - Altered binary operations on differently-indexed SparseSeries objects to use
    the integer-based (dense) alignment logic which is faster with a larger
    number of blocks (GH #205)
  - Refactored `Series.__repr__` to be a bit more clean and consistent

**API Changes**

  - `Series.describe` and `DataFrame.describe` now bring the 25% and 75%
    quartiles instead of the 10% and 90% deciles. The other outputs have not
    changed
  - `Series.toString` will print deprecation warning, has been de-camelCased to
    `to_string`

**Bug fixes**

  - Fix broken interaction between `Index` and `Int64Index` when calling
    intersection. Implement `Int64Index.intersection`
  - `MultiIndex.sortlevel` discarded the level names (GH #202)
  - Fix bugs in groupby, join, and append due to improper concatenation of
    `MultiIndex` objects (GH #201)
  - Fix regression from 0.4.1, `isnull` and `notnull` ceased to work on other
    kinds of Python scalar objects like `datetime.datetime`
  - Raise more helpful exception when attempting to write empty DataFrame or
    LongPanel to `HDFStore` (GH #204)
  - Use stdlib csv module to properly escape strings with commas in
    `DataFrame.to_csv` (PR #206, Thomas Kluyver)
  - Fix Python ndarray access in Cython code for sparse blocked index integrity
    check
  - Fix bug writing Series to CSV in Python 3 (PR #209)
  - Miscellaneous Python 3 bugfixes

Thanks
------

  - Thomas Kluyver
  - rsamson

pandas 0.4.2
============

Release notes
-------------

**Release date:** 10/3/2011

This is a performance optimization release with several bug fixes. The new
Int64Index and new merging / joining Cython code and related Python
infrastructure are the main new additions

**New features / modules**

  - Added fast `Int64Index` type with specialized join, union,
    intersection. Will result in significant performance enhancements for
    int64-based time series (e.g. using NumPy's datetime64 one day) and also
    faster operations on DataFrame objects storing record array-like data.
  - Refactored `Index` classes to have a `join` method and associated data
    alignment routines throughout the codebase to be able to leverage optimized
    joining / merging routines.
  - Added `Series.align` method for aligning two series with choice of join
    method
  - Wrote faster Cython data alignment / merging routines resulting in
    substantial speed increases
  - Added `is_monotonic` property to `Index` classes with associated Cython
    code to evaluate the monotonicity of the `Index` values
  - Add method `get_level_values` to `MultiIndex`
  - Implemented shallow copy of `BlockManager` object in `DataFrame` internals

**Improvements to existing features**

  - Improved performance of `isnull` and `notnull`, a regression from v0.3.0
    (GH #187)
  - Wrote templating / code generation script to auto-generate Cython code for
    various functions which need to be available for the 4 major data types
    used in pandas (float64, bool, object, int64)
  - Refactored code related to `DataFrame.join` so that intermediate aligned
    copies of the data in each `DataFrame` argument do not need to be
    created. Substantial performance increases result (GH #176)
  - Substantially improved performance of generic `Index.intersection` and
    `Index.union`
  - Improved performance of `DateRange.union` with overlapping ranges and
    non-cacheable offsets (like Minute). Implemented analogous fast
    `DateRange.intersection` for overlapping ranges.
  - Implemented `BlockManager.take` resulting in significantly faster `take`
    performance on mixed-type `DataFrame` objects (GH #104)
  - Improved performance of `Series.sort_index`
  - Significant groupby performance enhancement: removed unnecessary integrity
    checks in DataFrame internals that were slowing down slicing operations to
    retrieve groups
  - Added informative Exception when passing dict to DataFrame groupby
    aggregation with axis != 0

**API Changes**

None

**Bug fixes**

  - Fixed minor unhandled exception in Cython code implementing fast groupby
    aggregation operations
  - Fixed bug in unstacking code manifesting with more than 3 hierarchical
    levels
  - Throw exception when step specified in label-based slice (GH #185)
  - Fix isnull to correctly work with np.float32. Fix upstream bug described in
    GH #182
  - Finish implementation of as_index=False in groupby for DataFrame
    aggregation (GH #181)
  - Raise SkipTest for pre-epoch HDFStore failure. Real fix will be sorted out
    via datetime64 dtype

Thanks
------

- Uri Laserson
- Scott Sinclair

pandas 0.4.1
============

Release notes
-------------

**Release date:** 9/25/2011

This is primarily a bug fix release but includes some new features and
improvements

**New features / modules**

  - Added new `DataFrame` methods `get_dtype_counts` and property `dtypes`
  - Setting of values using ``.ix`` indexing attribute in mixed-type DataFrame
    objects has been implemented (fixes GH #135)
  - `read_csv` can read multiple columns into a `MultiIndex`. DataFrame's
    `to_csv` method will properly write out a `MultiIndex` which can be read
    back (PR #151, thanks to Skipper Seabold)
  - Wrote fast time series merging / joining methods in Cython. Will be
    integrated later into DataFrame.join and related functions
  - Added `ignore_index` option to `DataFrame.append` for combining unindexed
    records stored in a DataFrame

**Improvements to existing features**

  - Some speed enhancements with internal Index type-checking function
  - `DataFrame.rename` has a new `copy` parameter which can rename a DataFrame
    in place
  - Enable unstacking by level name (PR #142)
  - Enable sortlevel to work by level name (PR #141)
  - `read_csv` can automatically "sniff" other kinds of delimiters using
    `csv.Sniffer` (PR #146)
  - Improved speed of unit test suite by about 40%
  - Exception will not be raised calling `HDFStore.remove` on non-existent node
    with where clause
  - Optimized `_ensure_index` function resulting in performance savings in
    type-checking Index objects

**API Changes**

None

**Bug fixes**

  - Fixed DataFrame constructor bug causing downstream problems (e.g. .copy()
    failing) when passing a Series as the values along with a column name and
    index
  - Fixed single-key groupby on DataFrame with as_index=False (GH #160)
  - `Series.shift` was failing on integer Series (GH #154)
  - `unstack` methods were producing incorrect output in the case of duplicate
    hierarchical labels. An exception will now be raised (GH #147)
  - Calling `count` with level argument caused reduceat failure or segfault in
    earlier NumPy (GH #169)
  - Fixed `DataFrame.corrwith` to automatically exclude non-numeric data (GH
    #144)
  - Unicode handling bug fixes in `DataFrame.to_string` (GH #138)
  - Excluding OLS degenerate unit test case that was causing platform specific
    failure (GH #149)
  - Skip blosc-dependent unit tests for PyTables < 2.2 (PR #137)
  - Calling `copy` on `DateRange` did not copy over attributes to the new object
    (GH #168)
  - Fix bug in `HDFStore` in which Panel data could be appended to a Table with
    different item order, thus resulting in an incorrect result read back

Thanks
------
- Yaroslav Halchenko
- Jeff Reback
- Skipper Seabold
- Dan Lovell
- Nick Pentreath

pandas 0.4.0
============

Release notes
-------------

**Release date:** 9/12/2011

**New features / modules**

  - `pandas.core.sparse` module: "Sparse" (mostly-NA, or some other fill value)
    versions of `Series`, `DataFrame`, and `Panel`. For low-density data, this
    will result in significant performance boosts, and smaller memory
    footprint. Added `to_sparse` methods to `Series`, `DataFrame`, and
    `Panel`. See online documentation for more on these
  - Fancy indexing operator on Series / DataFrame, e.g. via .ix operator. Both
    getting and setting of values is supported; however, setting values will only
    currently work on homogeneously-typed DataFrame objects. Things like:

    * series.ix[[d1, d2, d3]]
    * frame.ix[5:10, ['C', 'B', 'A']], frame.ix[5:10, 'A':'C']
    * frame.ix[date1:date2]

  - Significantly enhanced `groupby` functionality

    * Can groupby multiple keys, e.g. df.groupby(['key1', 'key2']). Iteration with
      multiple groupings products a flattened tuple
    * "Nuisance" columns (non-aggregatable) will automatically be excluded from
      DataFrame aggregation operations
    * Added automatic "dispatching to Series / DataFrame methods to more easily
      invoke methods on groups. e.g. s.groupby(crit).std() will work even though
      `std` is not implemented on the `GroupBy` class

  - Hierarchical / multi-level indexing

    * New the `MultiIndex` class. Integrated `MultiIndex` into `Series` and
      `DataFrame` fancy indexing, slicing, __getitem__ and __setitem,
      reindexing, etc. Added `level` keyword argument to `groupby` to enable
      grouping by a level of a `MultiIndex`

  - New data reshaping functions: `stack` and `unstack` on DataFrame and Series

    * Integrate with MultiIndex to enable sophisticated reshaping of data

  - `Index` objects (labels for axes) are now capable of holding tuples
  - `Series.describe`, `DataFrame.describe`: produces an R-like table of summary
    statistics about each data column
  - `DataFrame.quantile`, `Series.quantile` for computing sample quantiles of data
    across requested axis
  - Added general `DataFrame.dropna` method to replace `dropIncompleteRows` and
    `dropEmptyRows`, deprecated those.
  - `Series` arithmetic methods with optional fill_value for missing data,
    e.g. a.add(b, fill_value=0). If a location is missing for both it will still
    be missing in the result though.
  - fill_value option has been added to `DataFrame`.{add, mul, sub, div} methods
    similar to `Series`
  - Boolean indexing with `DataFrame` objects: data[data > 0.1] = 0.1 or
    data[data> other] = 1.
  - `pytz` / tzinfo support in `DateRange`

    * `tz_localize`, `tz_normalize`, and `tz_validate` methods added

  - Added `ExcelFile` class to `pandas.io.parsers` for parsing multiple sheets out
    of a single Excel 2003 document
  - `GroupBy` aggregations can now optionally *broadcast*, e.g. produce an object
    of the same size with the aggregated value propagated
  - Added `select` function in all data structures: reindex axis based on
    arbitrary criterion (function returning boolean value),
    e.g. frame.select(lambda x: 'foo' in x, axis=1)
  - `DataFrame.consolidate` method, API function relating to redesigned internals
  - `DataFrame.insert` method for inserting column at a specified location rather
    than the default __setitem__ behavior (which puts it at the end)
  - `HDFStore` class in `pandas.io.pytables` has been largely rewritten using
    patches from Jeff Reback from others. It now supports mixed-type `DataFrame`
    and `Series` data and can store `Panel` objects. It also has the option to
    query `DataFrame` and `Panel` data. Loading data from legacy `HDFStore`
    files is supported explicitly in the code
  - Added `set_printoptions` method to modify appearance of DataFrame tabular
    output
  - `rolling_quantile` functions; a moving version of `Series.quantile` /
    `DataFrame.quantile`
  - Generic `rolling_apply` moving window function
  - New `drop` method added to `Series`, `DataFrame`, etc. which can drop a set of
    labels from an axis, producing a new object
  - `reindex` methods now sport a `copy` option so that data is not forced to be
    copied then the resulting object is indexed the same
  - Added `sort_index` methods to Series and Panel. Renamed `DataFrame.sort`
    to `sort_index`. Leaving `DataFrame.sort` for now.
  - Added ``skipna`` option to statistical instance methods on all the data
    structures
  - `pandas.io.data` module providing a consistent interface for reading time
    series data from several different sources

**Improvements to existing features**

  * The 2-dimensional `DataFrame` and `DataMatrix` classes have been extensively
    redesigned internally into a single class `DataFrame`, preserving where
    possible their optimal performance characteristics. This should reduce
    confusion from users about which class to use.

    * Note that under the hood there is a new essentially "lazy evaluation"
      scheme within respect to adding columns to DataFrame. During some
      operations, like-typed blocks will be "consolidated" but not before.

  * `DataFrame` accessing columns repeatedly is now significantly faster than
    `DataMatrix` used to be in 0.3.0 due to an internal Series caching mechanism
    (which are all views on the underlying data)
  * Column ordering for mixed type data is now completely consistent in
    `DataFrame`. In prior releases, there was inconsistent column ordering in
    `DataMatrix`
  * Improved console / string formatting of DataMatrix with negative numbers
  * Improved tabular data parsing functions, `read_table` and `read_csv`:

    * Added `skiprows` and `na_values` arguments to `pandas.io.parsers` functions
      for more flexible IO
    * `parseCSV` / `read_csv` functions and others in `pandas.io.parsers` now can
      take a list of custom NA values, and also a list of rows to skip

  * Can slice `DataFrame` and get a view of the data (when homogeneously typed),
    e.g. frame.xs(idx, copy=False) or frame.ix[idx]
  * Many speed optimizations throughout `Series` and `DataFrame`
  * Eager evaluation of groups when calling ``groupby`` functions, so if there is
    an exception with the grouping function it will raised immediately versus
    sometime later on when the groups are needed
  * `datetools.WeekOfMonth` offset can be parameterized with `n` different than 1
    or -1.
  * Statistical methods on DataFrame like `mean`, `std`, `var`, `skew` will now
    ignore non-numerical data. Before a not very useful error message was
    generated. A flag `numeric_only` has been added to `DataFrame.sum` and
    `DataFrame.count` to enable this behavior in those methods if so desired
    (disabled by default)
  * `DataFrame.pivot` generalized to enable pivoting multiple columns into a
    `DataFrame` with hierarchical columns
  * `DataFrame` constructor can accept structured / record arrays
  * `Panel` constructor can accept a dict of DataFrame-like objects. Do not
    need to use `from_dict` anymore (`from_dict` is there to stay, though).

**API Changes**

  * The `DataMatrix` variable now refers to `DataFrame`, will be removed within
    two releases
  * `WidePanel` is now known as `Panel`. The `WidePanel` variable in the pandas
    namespace now refers to the renamed `Panel` class
  * `LongPanel` and `Panel` / `WidePanel` now no longer have a common
    subclass. `LongPanel` is now a subclass of `DataFrame` having a number of
    additional methods and a hierarchical index instead of the old
    `LongPanelIndex` object, which has been removed. Legacy `LongPanel` pickles
    may not load properly
  * Cython is now required to build `pandas` from a development branch. This was
    done to avoid continuing to check in cythonized C files into source
    control. Builds from released source distributions will not require Cython
  * Cython code has been moved up to a top level `pandas/src` directory. Cython
    extension modules have been renamed and promoted from the `lib` subpackage to
    the top level, i.e.

    * `pandas.lib.tseries` -> `pandas._tseries`
    * `pandas.lib.sparse` -> `pandas._sparse`

  * `DataFrame` pickling format has changed. Backwards compatibility for legacy
    pickles is provided, but it's recommended to consider PyTables-based
    `HDFStore` for storing data with a longer expected shelf life
  * A `copy` argument has been added to the `DataFrame` constructor to avoid
    unnecessary copying of data. Data is no longer copied by default when passed
    into the constructor
  * Handling of boolean dtype in `DataFrame` has been improved to support storage
    of boolean data with NA / NaN values. Before it was being converted to float64
    so this should not (in theory) cause API breakage
  * To optimize performance, Index objects now only check that their labels are
    unique when uniqueness matters (i.e. when someone goes to perform a
    lookup). This is a potentially dangerous tradeoff, but will lead to much
    better performance in many places (like groupby).
  * Boolean indexing using Series must now have the same indices (labels)
  * Backwards compatibility support for begin/end/nPeriods keyword arguments in
    DateRange class has been removed
  * More intuitive / shorter filling aliases `ffill` (for `pad`) and `bfill` (for
    `backfill`) have been added to the functions that use them: `reindex`,
    `asfreq`, `fillna`.
  * `pandas.core.mixins` code moved to `pandas.core.generic`
  * `buffer` keyword arguments (e.g. `DataFrame.toString`) renamed to `buf` to
    avoid using Python built-in name
  * `DataFrame.rows()` removed (use `DataFrame.index`)
  * Added deprecation warning to `DataFrame.cols()`, to be removed in next release
  * `DataFrame` deprecations and de-camelCasing: `merge`, `asMatrix`,
    `toDataMatrix`, `_firstTimeWithValue`, `_lastTimeWithValue`, `toRecords`,
    `fromRecords`, `tgroupby`, `toString`
  * `pandas.io.parsers` method deprecations

    * `parseCSV` is now `read_csv` and keyword arguments have been de-camelCased
    * `parseText` is now `read_table`
    * `parseExcel` is replaced by the `ExcelFile` class and its `parse` method

  * `fillMethod` arguments (deprecated in prior release) removed, should be
    replaced with `method`
  * `Series.fill`, `DataFrame.fill`, and `Panel.fill` removed, use `fillna`
    instead
  * `groupby` functions now exclude NA / NaN values from the list of groups. This
    matches R behavior with NAs in factors e.g. with the `tapply` function
  * Removed `parseText`, `parseCSV` and `parseExcel` from pandas namespace
  * `Series.combineFunc` renamed to `Series.combine` and made a bit more general
    with a `fill_value` keyword argument defaulting to NaN
  * Removed `pandas.core.pytools` module. Code has been moved to
    `pandas.core.common`
  * Tacked on `groupName` attribute for groups in GroupBy renamed to `name`
  * Panel/LongPanel `dims` attribute renamed to `shape` to be more conformant
  * Slicing a `Series` returns a view now
  * More Series deprecations / renaming: `toCSV` to `to_csv`, `asOf` to `asof`,
    `merge` to `map`, `applymap` to `apply`, `toDict` to `to_dict`,
    `combineFirst` to `combine_first`. Will print `FutureWarning`.
  * `DataFrame.to_csv` does not write an "index" column label by default
    anymore since the output file can be read back without it. However, there
    is a new ``index_label`` argument. So you can do ``index_label='index'`` to
    emulate the old behavior
  * `datetools.Week` argument renamed from `dayOfWeek` to `weekday`
  * `timeRule` argument in `shift` has been deprecated in favor of using the
    `offset` argument for everything. So you can still pass a time rule string
    to `offset`

**Bug fixes**

  * Column ordering in `pandas.io.parsers.parseCSV` will match CSV in the presence
    of mixed-type data
  * Fixed handling of Excel 2003 dates in `pandas.io.parsers`
  * `DateRange` caching was happening with high resolution `DateOffset` objects,
    e.g. `DateOffset(seconds=1)`. This has been fixed
  * Fixed __truediv__ issue in `DataFrame`
  * Fixed `DataFrame.toCSV` bug preventing IO round trips in some cases
  * Fixed bug in `Series.plot` causing matplotlib to barf in exceptional cases
  * Disabled `Index` objects from being hashable, like ndarrays
  * Added `__ne__` implementation to `Index` so that operations like ts[ts != idx]
    will work
  * Added `__ne__` implementation to `DataFrame`
  * Bug / unintuitive result when calling `fillna` on unordered labels
  * Bug calling `sum` on boolean DataFrame
  * Bug fix when creating a DataFrame from a dict with scalar values
  * Series.{sum, mean, std, ...} now return NA/NaN when the whole Series is NA
  * NumPy 1.4 through 1.6 compatibility fixes
  * Fixed bug in bias correction in `rolling_cov`, was affecting `rolling_corr`
    too
  * R-square value was incorrect in the presence of fixed and time effects in
    the `PanelOLS` classes
  * `HDFStore` can handle duplicates in table format, will take

Thanks
------
  - Joon Ro
  - Michael Pennington
  - Chris Uga
  - Chris Withers
  - Jeff Reback
  - Ted Square
  - Craig Austin
  - William Ferreira
  - Daniel Fortunov
  - Tony Roberts
  - Martin Felder
  - John Marino
  - Tim McNamara
  - Justin Berka
  - Dieter Vandenbussche
  - Shane Conway
  - Skipper Seabold
  - Chris Jordan-Squire

pandas 0.3.0
============

This major release of pandas represents approximately 1 year of continuous
development work and brings with it many new features, bug fixes, speed
enhancements, and general quality-of-life improvements. The most significant
change from the 0.2 release has been the completion of a rigorous unit test
suite covering all of the core functionality.

Release notes
-------------

**Release date:** February 20, 2011

**New features / modules**

* DataFrame / DataMatrix classes

 * `corrwith` function to compute column- or row-wise correlations between two
   objects
 * Can boolean-index DataFrame objects, e.g. df[df > 2] = 2, px[px > last_px] = 0
 * Added comparison magic methods (__lt__, __gt__, etc.)
 * Flexible explicit arithmetic methods (add, mul, sub, div, etc.)
 * Added `reindex_like` method

* WidePanel

 * Added `reindex_like` method

* `pandas.io`: IO utilities

  * `pandas.io.sql` module

    * Convenience functions for accessing SQL-like databases

  * `pandas.io.pytables` module

   * Added (still experimental) HDFStore class for storing pandas data
     structures using HDF5 / PyTables

* `pandas.core.datetools`

  * Added WeekOfMonth date offset

* `pandas.rpy` (experimental) module created, provide some interfacing /
  conversion between rpy2 and pandas

**Improvements**

* Unit test coverage: 100% line coverage of core data structures

* Speed enhancement to rolling_{median, max, min}

* Column ordering between DataFrame and DataMatrix is now consistent: before
  DataFrame would not respect column order

* Improved {Series, DataFrame}.plot methods to be more flexible (can pass
  matplotlib Axis arguments, plot DataFrame columns in multiple subplots, etc.)

**API Changes**

* Exponentially-weighted moment functions in `pandas.stats.moments`
  have a more consistent API and accept a min_periods argument like
  their regular moving counterparts.

* **fillMethod** argument in Series, DataFrame changed to **method**,
  `FutureWarning` added.

* **fill** method in Series, DataFrame/DataMatrix, WidePanel renamed to
  **fillna**, `FutureWarning` added to **fill**

* Renamed **DataFrame.getXS** to **xs**, `FutureWarning` added

* Removed **cap** and **floor** functions from DataFrame, renamed to
  **clip_upper** and **clip_lower** for consistency with NumPy

**Bug fixes**

* Fixed bug in IndexableSkiplist Cython code that was breaking
  rolling_max function

* Numerous numpy.int64-related indexing fixes

* Several NumPy 1.4.0 NaN-handling fixes

* Bug fixes to pandas.io.parsers.parseCSV

* Fixed `DateRange` caching issue with unusual date offsets

* Fixed bug in `DateRange.union`

* Fixed corner case in `IndexableSkiplist` implementation
