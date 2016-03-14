# csv-tools
Basic CSV file processing tools, as shell scripts, piggybacked on PHP's CSV
parsing functions

**csv-to-tsv** and **csv-from-tsv** are simple converters for comma-separated
format files into tab-separated format. Tab characters are much less common in
the field values themselves, so this makes further processing a lot more
robust. For example, `awk` can be set to use tabs as separators and this opens
a world of flexibiltity for further processing. If the field values contain
commas and the `awk` separator is set to a comma, `awk` can't tell whether the
comma it encounters on a line is a separator or part of a real value.
