# csv-tools
Basic CSV file processing tools, as shell scripts, piggybacked on PHP's CSV
parsing functions.

All scripts expect data over stdin and will return their output on stdout. They
make an effort to be minimally resource intensive as far as possible, operating
on the input stream line-by-line rather than reading the whole data set at
once. The only script that reads a whole data set in one go is `csv-merge`,
which only reads one of the data sets and has a memory limit tweak to
accommodate this for relatively large files.

**csv-to-tsv** and **csv-from-tsv** are simple converters for comma-separated
format files into tab-separated format. Tab characters are much less common in
the field values themselves, so this makes further processing a lot more
robust. For example, `awk` can be set to use tabs as separators and this opens
a world of flexibiltity for further processing. If the field values contain
commas and the `awk` separator is set to a comma, `awk` can't tell whether the
comma it encounters on a line is a separator or part of a real value.

**csv-headings** returns the contents of the first line of the file as a base-1
numbered list. Normally one would use this to read the headings in a file.

**csv-cut** expects as its argument a comma separated list of base-1 indexes
for the fields to extract from the data. If there is no value in the data, a
blank is returned for that field. This tool can also be used to re-arrange
fields as the fields listed are returned in the *listed* order, not the source
data order.

**csv-merge** expects two filenames on the command line, rather than using
stdin. CSV data is returned on stdout. The first column is expected to contain
the identifier and the value of this column will be used as the match. The data
from the second file is appended as subsequent columns on the data from the
first file. The indentifier is not repeated. The `csv-merge` tool behaves as
follows:

- If the identifiers in the second file are non-unique, the data for the last
  occurrence of the identifier is used
- If the identifiers in the first file are non-unique, the data from the second
  file is appended to each row where the identifier matched
- If the identifier exists in the first file but not in the second, the output
  data will contain blanks for the columns that should have been added by the
  second file
- If the identifier exists in the second file but not in the first, the output
  data will not contain the data for this identifier
