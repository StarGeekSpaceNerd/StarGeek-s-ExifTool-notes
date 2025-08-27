**Under construction and incomplete**

# The exiftool CSV option
The way the CSV option works in exiftool can be a bit confusing.

The first thing to do is read the docs on the [`-csv` option](https://exiftool.org/exiftool_pod.html#csv-CSVFILE) as well as [FAQ #26, "How do I import information from a database?"](https://exiftool.org/faq.html#Q26).

Exiftool requires the CSV file to be in a specific format. The first row has the names of the tags that will be written. The first column is a special column called "SourceFile".

Here's an example
`SourceFile,DateTimeOriginal,Keywords
Y:\!temp\x\y\Test4.jpg,2024:09:27 12:00:00,"Keywords 1, Keyword 2"`

"SourceFile" can either be an absolute path to the file or it can be a relative path. The relative path will be to the current directory exiftool is running from. For example, the "SourceFile" column has only the filename, such as Test4.jpg in the above example, then you must run exiftool from the directory that Test4.jpg is in. If all the files are in different subdiretories, and CSV only has the filenames and no paths, then exiftool will not be able to write the data from the CSV file (though see the symlink workaround below).

The CSV file is **NOT** a list of files to add data to. Instead, it is a lookup table. The files or the directories the files are in still need to be listed on the command line. Exiftool will then take each file it is processing and check the CSV file to see if it is listed. If it find a correct listing, it will then embed the data from that row into the file.

## Advance processing
### Symlink workaround
To be added