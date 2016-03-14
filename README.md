# csv-tools
Basic CSV file processing tools, as shell scripts, piggybacked on PHP's CSV
parsing functions.

All scripts expect data over stdin and will return their output on stdout.

**csv-to-tsv** and **csv-from-tsv** are simple converters for comma-separated
format files into tab-separated format. Tab characters are much less common in
the field values themselves, so this makes further processing a lot more
robust. For example, `awk` can be set to use tabs as separators and this opens
a world of flexibiltity for further processing. If the field values contain
commas and the `awk` separator is set to a comma, `awk` can't tell whether the
comma it encounters on a line is a separator or part of a real value.

**csv-headings** returns the contents of the first line of the file as a base-1
numbered list. Normally one would use this to read the headings in a file.
