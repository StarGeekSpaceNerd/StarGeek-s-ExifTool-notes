StarGeek's exiftool notes
===
These are my unsorted notes and links to various use exiftool posts.

# Unsorted notes

## "Lost" ebv4linux interview with Phil
In German, can be translated with web browser translation abilities
https://web.archive.org/web/20150419003745/http://www.ebv4linux.de/modules.php?name=News&file=article&sid=26

## "Shifting" non-shiftable composite date/time tags
Composite date/time tags such `SubSecDateTimeOriginal` are not shiftable by using `-=`/`+=`.  To work around, use the `ShiftTime` helper function
`"-SubSecDateTimeOriginal<${SubSecDateTimeOriginal;ShiftTime('-0:0:10')"`
https://exiftool.org/forum/index.php?msg=78691

## "Undocumented" subroutines
Technically documented in the source code, but theses aren't really documented outside of that.
These can be found in `ExifTool.pm`

- TimeZoneString
- ConvertUnixTime
- GetUnixTime

Post to refer to with regards to figuring out time zone

## `-TagsFromFile` and `-All:All` / `-All`
Working out the difference between various `-GROUP:All` tag copies
https://exiftool.org/forum/index.php?msg=79962

## A discussion on deleting metadata
https://exiftool.org/forum/index.php?msg=76627

## Access another tag from within advanced formatting
This way should not be used, Needs rewriting.  Instead, `$self->GetValue('tag')` should be used
https://exiftool.org/forum/index.php?msg=34104

`$$self{VALUE}{TAG}`

For example, to remove Make from within the Model tag

`exiftool "-title<${Model;s/\\\\s\\\*$$self{VALUE}{Make}\\\\s\\\*//i}" -m`

This uses ExifTool internals feature to access the Make tag from within the advanced formatting expression for Model.  But a disadvantage of doing it this way is that you will get a warning due to an uninitialized value in this expression if Make doesn't exist, hence the -m option. The tag is case sensitive.

## ACDSee regions and sample image
Sample image with ACDSee regions
https://exiftool.org/forum/index.php?msg=57132

## Add tag to all files that have matching file in different folder
Example, for every jpg in `/path/to/published/2015/`, exiftool will check in `/path/to/library/` for a file with the same name and add "2015" to the `Subject` tag in the matching file
`exiftool -subject+=2015 -ext jpg -srcfile /path/to/library/%f.%e /path/to/published/2015/`
https://exiftool.org/forum/index.php?msg=76725

## Adding Date/Time to What's App image
https://exiftool.org/forum/index.php?msg=77199
or
https://exiftool.org/forum/index.php?msg=64777

## Adding directory path to keywords
https://exiftool.org/forum/index.php?msg=49360

## Appending a CSV file
https://exiftool.org/forum/index.php?msg=76086

## Apple doesn't understand metadata links
Links showing times when Apple incorrectly deals with metadata
To do, dig up links on this
Wildly inaccurate date/time in Apple Photos with date/time Time stamps missing time zone
https://exiftool.org/forum/index.php?msg=56769
with images
https://exiftool.org/forum/index.php?msg=64363

## Apple Photos Quicktime Timezone error
Wildly inaccurate date/time in Apple Photos with date/time Time stamps missing time zone
https://exiftool.org/forum/index.php?msg=56769
with images
https://exiftool.org/forum/index.php?msg=64363

## AVIDemux settings to remove all metadata
AVIDemux doesn't copy any metadata, so it can be used to remove all the metadata, even those that exiftool can't remove such as a GPS track or EXIF data
https://exiftool.org/forum/index.php?msg=64673

## Changing extension to Title Case
This will upper case the first letter, then lower case the rest
`-Filename=%f.%1ue%.1le`

## Converting a local time to UTC
Needs expansion and updated with the standard exiftool routines

Requires that the `OffsetTime*` tag is set
`${SubSecDateTimeOriginal#;use POSIX qw(strftime);DateFmt('%s');$_=strftime('%Y-%m-%d_%H-%M-%S',gmtime($_))}`
https://exiftool.org/forum/index.php?msg=79228

## Copy metadata from one file to another with completely different names using hardlinks to sync them
A multistep operation to copy tags from one directory to another where the files have all been renamed and cannot be linked by editing the name, but can be linked by a tag, in this case `Duration`. This procedure creates hard links with names based upon `Duration` and allows copying the data based upon that.
https://exiftool.org/forum/index.php?msg=68166

## Copy of the Metadata Working Group
A copy of the Metadata Working Group PDF
https://exiftool.org/forum/index.php?msg=53039
Additionally, via Archive.org
https://web.archive.org/web/20180919181934/http://www.metadataworkinggroup.org/pdf/mwg_guidance.pdf

## Copy time stamps from source video to new video
`exiftool -TagsFromFile source.mp4 "-all:all<time:all" target.mp4`
https://exiftool.org/forum/index.php?msg=78133

## CR3 files are MP4 based
> CR3 is based on the MOV/MP4 video format

https://exiftool.org/forum/index.php?msg=77238

## Creating tags with dots in the name
Two similar posts
https://exiftool.org/forum/index.php?msg=26531
https://exiftool.org/forum/index.php?msg=66841

## Dealing with different time zones and video UTC
Original thread where the [`-api TimeZone` option](https://exiftool.org/ExifTool.html#TimeZone) was added
https://exiftool.org/forum/index.php?msg=44700
My updated example post, where I detail problems with Windows extremely poor handing of time zones
https://exiftool.org/forum/index.php?msg=75768

## Dealing with the need for multiple `-sep` characters
Use `tr///` or `s///` to change them all so you can use only one `-sep` option
https://exiftool.org/forum/index.php?msg=82500

## Details on which time stamps should be Local vs UTC
This can probably be expanded
https://exiftool.org/forum/index.php?msg=75031

## DirOpus rename button example
https://exiftool.org/forum/index.php?msg=6243

## Does the MWG (Metadata Working Group) still exist
Answer, probably not anymore
Still exists 2019
https://exiftool.org/forum/index.php?msg=52224
Still no change 2020
https://exiftool.org/forum/index.php?msg=58151

## Don't use PDF:Keywords with commas
https://exiftool.org/forum/index.php?msg=80503

## EXIF in MOV/MP4 files is non-standard
EXIF data is non-standard in files and will be lost if the file is edited. The best workaround would be to use the [`exif2xmp.args` file](https://github.com/exiftool/exiftool/blob/master/arg_files/exif2xmp.args) to copy the data to the corrisponding tags in XMP
https://exiftool.org/forum/index.php?msg=56282

## Exiftool calculates `Duration` Incorrectly
Exiftool calculates the `Duration` based upon the header metadata and doesn't analyze the stream itself.  If the header has incorrect data, then the value could be off.
https://github.com/exiftool/exiftool/issues/160#issuecomment-1293946184

## Exiftool Group tag names
The group names can be found under the
`GetGroup` function or using -listg
https://exiftool.org/ExifTool.html#GetAllGroups

## Exiftool startup time/Common Mistake 3
Christian Etter has done some timing tests with the Windows exiftool.exe application, and has determined that for his set of test images the startup overhead of running exiftool on each image separately accounts for 98.4% of the execution time. This means that you can get a speed-up factor of 60x by running exiftool in batch mode on a large set of images, rather than executing it separately for each image.
https://exiftool.org/forum/index.php?msg=6121
Blog post via Archive.org
https://web.archive.org/web/20120223091305/http://www.christian-etter.de/?p=458

## Extract Images from a PDF
https://exiftool.org/forum/index.php?msg=31010
https://exiftool.org/exiftool_pod.html#exiftool--a--b--ee--embeddedimage--W-Image_-.3g3.-s-file.pdf
Example:
`exiftool -ee -embeddedimage -b -W %t%c.%s some.pdf`

## Extracting GPS data from MP4 video
Original megathread
https://exiftool.org/forum/index.php?msg=45447

Otherwise now documented under [Inverse Geotagging](https://exiftool.org/geotag.html#Inverse)

## Find all images within X distance of GPS Coordinates
https://exiftool.org/forum/index.php?msg=59031

## Flickr uses Exiftool
https://code.flickr.net/2012/06/01/parsing-exif-client-side-using-javascript-2/

## garbage at end of string in strptime
Not useful? Delete?
https://exiftool.org/forum/index.php?msg=63144

## Generate a user-defined tag only if requested
https://exiftool.org/forum/index.php?msg=64462

## Google Takeout, Rename JSON files to correct copy number location in filename
**Google does NOT remove data from your files**
**Always double check your files to make sure you're not overwriting data that was never removed**
The file system time stamps are ususally the only thing that "needs" to be fixed, and that can be done by copying the time stamps from the embedded tags, such as `DateTimeOriginal`
https://exiftool.org/forum/index.php?msg=68268

## googlemap kml export
Windows bat file to create KML file for Google Earth with icons
https://exiftool.org/forum/index.php?msg=72535

## GPS and EXIF data in a video, copy/paste

My standard copy/paste when it comes to EXIF/GPS data in a video
\[hr\]
The problem is that there really isn't a standard for embedding a GPS track in a video\* Currently, exiftool reads \*\*74 different ways\*\* that a GPS track can be in a video and there are about half a dozen more in which the format hasn't been decoded. I have yet to find a program that will embed a GPS track into a video file.

And that won't be the only data you will lose when recompressing a video. The same situation exists with the EXIF data that is written into the video. Most video data is \[url=https://exiftool.org/TagNames/QuickTime.html\]Quicktime data\[/url\] and EXIF data in a video file is non-standard. But camera companies shove it in there anyway, with each company doing it in different ways.

The best you can do is extract the GPS data into a GPX track and copy the EXIF data into the corresponding XMP tags (see the [url=https://github.com/exiftool/exiftool/blob/master/arg_files/exif2xmp.args]\[tt\]exif2xmp.args\[/tt\] file\[/url\] on GitHub), which are allowed in a video file.

\*Technically, there is a standard by Google, but nobody follows it, and I've never found any software that write this format. I mention it in [url=https://exiftool.org/forum/index.php?msg=69582]this Exiftool forum's post\[/url\], which has a response from the author of exiftool

## GPS reference directions
Contains GIF of how to copy/paste GPS coordinates in a spreadsheet in order to create the Ref direction tags as well
https://exiftool.org/forum/index.php?msg=73550

## Historical, Parse H264 stream
Edit the source code to activate steam parsing
This is no longer needed. Using `-ee2` or higher activates it.
https://exiftool.org/forum/index.php?msg=65183

## Historical: Tom Christiansen (co-author of "Programming Perl") and dealing with UTF-8
https://exiftool.org/forum/index.php?msg=7642

## How to get first letter each word in a Tag (skips apostrophe)
Very old, Double check this.

`"${TAG;$_=join('',m/(?<!')\b(\w)/g);}"`
Upper case the letter
`"${TAG;$_=uc(join('',m/(?<!')\b(\w) /g));}"`

## How to pass an empty value with `-api missingtagvalue=`
Use `-api missingtagvalue^=`
https://exiftool.org/forum/index.php?msg=79260

Under Windows, this needs to be quoted, as the caret `^` is a special character in Windows CMD.

## How to upload 360 videos to google street video tutorial
I haven't tested this as I don't have access to need hardware/software
https://old.reddit.com/r/Insta360/comments/10ii9r3/how_to_upload_360_videos_to_google_street_video/

## Include other config files
\*\*I had problems using, need to ask Phil for clarification\*\*
https://exiftool.org/forum/index.php?msg=64453

Solution is `use`
https://exiftool.org/forum/index.php?msg=87014

## Increment the time stamp
https://exiftool.org/forum/index.php?msg=27394

Advanced version of incrementing time
https://exiftool.org/forum/index.php?msg=82058

## IPTCDigest - IPTCDigest is not current
https://exiftool.org/forum/index.php?msg=75864

## jonkeren's Exiftool Commands/cheat sheet
One exiftool user's cheat sheet
Some of these can be simplified or updated
https://github.com/jonkeren/Exiftool-Commands

## JPEG Snoop page with visuals on EXIF orientation
Oritinal page was taken down, link via Archive.org
https://web.archive.org/web/20180819022932/https://www.impulseadventure.com/photo/exif-orientation.html

## JSON output and numbers
> The values output by exiftool are not typed, which leads to problems when converting for the JSON output. If it looks like a number, then ExifTool writes a JSON number, otherwise it quotes it as a string.

https://exiftool.org/forum/index.php?msg=37780

## Keep it (tag names) simple
https://exiftool.org/forum/index.php?msg=80202

## Keeping alt-lang tags when updating
https://exiftool.org/forum/index.php?msg=60655

## List type tags: Example of how list type tags are separated/EXIF time stamps breakdown
https://exiftool.org/forum/index.php?msg=76017

## List type tags: What are List Type tags?

List type tags are tags which are saved in the file as individual separate entries.  While many programs will display them as comma/semi-colon separated, they are not.  Each entry is completely self contained and separate from the others.  An example of this can be easily seen by looking at the raw data in the file.  Here's what it looks like in  the `XMP-dc:Subject`  tag

```
<dc:subject>
 <rdf:Bag>
  <rdf:li>keyword 1</rdf:li>
  <rdf:li>keyword 2</rdf:li>
  <rdf:li>keyword , with comma</rdf:li>
 </rdf:Bag>
</dc:subject>
```

Bridge example:
![Bridge-2023-01-15_09.35.14.png](Bridge-2023-01-15_09.35.14.png)

## Looking at the details of a file
Examples of `-v` and `-htmldump` options
https://exiftool.org/forum/index.php?msg=74866

## Maker note tags documentation
> Maker note tags are reverse engineered by camera owners since there is no official documentation available (with rare exceptions).

https://exiftool.org/forum/index.php?msg=78692

## My escape html entities AutoIt3 script
https://exiftool.org/forum/index.php?msg=67755

## My opinion on using the [`-execute` option](https://exiftool.org/exiftool_pod.html#execute-NUM) on the command line
IMO, the `-execute` option is rarely useful combining a small number of commands. It doesn't create a single command, it simply runs more than one command without having to restart exiftool. And while the startup time is exiftool's biggest performance hit, it won't be that big of a hit if you're only combining two or three commands. Using it adds complexity and makes thing harder to troubleshoot if there's a problem with the command. It is less troublesome/error prone to simply run those command in sequence.
## Old post on avoiding corruption and how exiftool rewrites the file
https://exiftool.org/forum/index.php?msg=7493

## On leading numbers for groups
Copy/paste for details on leading numbers for groups
\[quote author=Archive link=msg=7187 date=1273668838\]The leading family number is almost never used.  The only reason it is
needed is to distinguish between the rare cases where a group has the same name but represents a different set of tags in family 0 and 1.  This only happens in the case where there are multiple IPTC records in a single file (which only happens when some proprietary information contiaining IPTC has been written to the file).  In this rare case, the family 0 group names of both IPTC records are "IPTC", while the family 1 group names are "IPTC" and "IPTC2".\[/quote\]

https://exiftool.org/forum/index.php?msg=7187

## Opinion on Dashcam manufacturers obfuscating the embedded data such as GPS tracks
https://exiftool.org/forum/index.php?msg=76061

## Order in which file types are checked
From 2022-10-25, may be outdated
https://exiftool.org/forum/index.php?msg=75821

## Orientation tags in .heic photo
`Orientation` and `Rotation` have interactions in MP4 based image files. Especially see GreyBeard's posts here
https://exiftool.org/forum/index.php?msg=81909

## Overwriting files with the `-o` (`-out`) option
https://exiftool.org/forum/index.php?msg=33172

## Partial date times
This will work with a filename with just the year, year and month, or year month and day
Phil's original
https://exiftool.org/forum/index.php?msg=34700
my version
https://exiftool.org/forum/index.php?msg=82406
I should have another version of mine but can't find it atm

## Performance hit with `Image::ExifTool` over time
https://exiftool.org/forum/index.php?msg=26069
https://exiftool.org/forum/index.php?msg=80020

## Perl script to run multiple exiftool commands in parallel
https://exiftool.org/forum/index.php?msg=39110

## Phil on adding GPS track to a video
https://exiftool.org/forum/index.php?msg=77473

## Phil on writing to PDFs
>There isn't much chance that I will add a permanent delete feature to ExifTool because the PDF structure is very complicated and doing this would be a lot of work.  Bascially, the only reason I was able to add a write feature for PDF at all is because I was able to do an incremental update (which avoids the problem of having to rewrite the entire file).
https://exiftool.org/forum/index.php?msg=21748

Additionally
It turns out there are 3 problems with this (removing all metadata):

1.  It is harder than I had hoped to simply zero out the existing metadata.

2.  The solution wouldn't be complete because there could already be unused objects containing old metadata in the original PDF, and ExifTool wouldn't be able to zero out these.

3.  It has been advertised that ExifTool PDF edits are reversible, and some users may be relying on this feature.

https://exiftool.org/forum/index.php?msg=54610

## Phil's `pp_build_exe.args` script to create Windows executable
https://exiftool.org/forum/index.php?msg=18798

## Phil's brute force image extraction script
https://exiftool.org/forum/index.php?msg=19805

## Phil's EBird page
https://exiftool.org/forum/index.php?msg=59975
https://media.ebird.org/catalog?userId=USER1671030&mediaType=photo

## Phil's ICAT Image Cataloging Tool
https://exiftool.org/icat/

## Phil's script to replace jpeg image without changing metadata
Phil uses this to remove images from the [ExifTool Meta Information Repository](https://exiftool.org/sample_images.html)
https://exiftool.org/forum/index.php?msg=8031

## Phil's `extract_preview` script
A perl script which attempts to extract preview jpgs from corrupted files
https://exiftool.org/forum/index.php?msg=19805

## PNG text chunks after the IDAT
In PNG images, Exiftool gives a warning when there are text chunks after the IDAT chunk. This is allowed by the spec (I think), but there are programs that cannot read chunks after the IDAT

> Web Browser vendors have decided that the eXIf chunk needs to be before image data, otherwise web browsers will ignore it: https://github.com/w3c/csswg-drafts/issues/4929

A good point is made there in that putting metadata after the image data is not compatable with streaming the image. The image would be displayed as it was downloaded, but then it would have to be rotated if the `Orienation` tag appeared after the image data

https://exiftool.org/forum/index.php?msg=68443

Writing the text chunks after the IDAT is something ImageMagick has done for many years
https://github.com/dlemstra/Magick.NET/discussions/1603#discussioncomment-9056185

## Possible help with Pano/Panorama  Video
https://exiftool.org/forum/index.php?msg=64971

## Powershell corrupts redirected/piped binary data
Earlier post on the subject
https://exiftool.org/forum/index.php?msg=22903
My post on the subject
https://exiftool.org/forum/index.php?msg=41663

## PowerShell sucks at quoting
https://exiftool.org/forum/index.php?msg=80581

## Quicktime delete date/time timestamps
https://exiftool.org/forum/index.php?msg=54897

## Regarding APP14 Adobe
The JPEG APP14 Adobe segment contains some color information that may severely affect the image appearance if deleted.
https://exiftool.org/forum/index.php?msg=32114

## Renaming files and XMP sidecars
https://exiftool.org/forum/index.php?msg=6201

## Set `.exiftool_config` to always show unknown tags
Example use of using different default [Options](https://exiftool.org/ExifTool.html#Options). Setting `LargeFileSupport` in this way is a common use.
https://exiftool.org/forum/index.php?msg=79956

## SIGMA and FOVEON EXIF MakerNote Documentation

Early information on Sigma Makernotes. Outdated, but historical from an era when a camera company actually shared their specs.
https://web.archive.org/web/20070805234644/http://www.x3f.info:80/technotes/FileDocs/MakerNoteDoc.html

## Simple BAT file for removing exiftool par directories
Thread also details how to make the old ExiftoolGUI portable, may not apply to current version
```
cd %temp%
for /d %%a in (*par*) do rd /s /q "%%a"
```
https://exiftool.org/forum/index.php?msg=12368

## Some examples using a unix time stamp
Example is that the filename was a unix time stamp and needed to be renamed to a more standard time stamp
This is messy and need further research on what is happening
https://exiftool.org/forum/index.php?msg=50605

## Sorting list type tags
simple case insensitive sort
https://exiftool.org/forum/index.php?topic=9420.0
More complex Natural Order compare
https://exiftool.org/forum/index.php?msg=83636
Code source
https://www.perlmonks.org/?node_id=540890

## Speed of using `-overwrite_original_in_place`
`-overwrite_original_in_place` should be roughly half the speed of `-overwrite_original` because it has to write the file twice
https://exiftool.org/forum/index.php?msg=77017

## Split directory path to get specific directory level
This requires the use of the full directory path on the command line. If using only the dot `.` as the directory path, use the `Filepath` tag and take note that the addition of the filename needs to be taken into account
https://exiftool.org/forum/index.php?msg=49791

## StackOverflow UTF8 GUI changes

Examples of how the StackOverflow Windows UTF8 option may affect GUIs
https://exiftool.org/forum/index.php?msg=72233

## System Timestamps prior to 1970
This problem has been fixed as of Version 12.84
(needs a re-write based upon last link)
ExifTool uses standard Perl date/time routines to do the necessary conversions. These routines are based on an epoch date of 1970, and the behavior before that can be funny.
it is very unlikely that you would have any digital files created before this time. If you want to set an earlier time you must be using the system date/time for something other than the intended purpose. Also note that you may have problems with these date/times if the files are transferred to different file systems.

- Nov 2017: https://exiftool.org/forum/index.php?msg=44652
- Jan 2018: https://exiftool.org/forum/index.php?msg=45528
- May 2018: https://exiftool.org/forum/index.php?msg=47458
- Aug 2018: https://exiftool.org/forum/index.php?msg=48623
- March 2019: https://exiftool.org/forum/index.php?msg=51768
- Nov 2022: https://exiftool.org/forum/index.php?msg=76647

Same problem with the addition of Quicktime time stamps and `-api QuickTimeUTC`
https://exiftool.org/forum/index.php?msg=82437

### Fixed formatted tags
An incomplete list of tags that would require overriding in order to write non-standard data. See this post
https://exiftool.org/forum/index.php?msg=76643
- `XMP-exif:GPSLatitude`
- `XMP-exif:GPSLongitude`

## To do, explain why there may be differences in GPS Coordinate written compared to what is read, and why the EXIF GPS coordinates may be different than the XMP ones. Also, Accuracy of decimal places/how many decimals are too many
Need to consolidate and simplify these
Early post on differences
https://exiftool.org/forum/index.php?msg=7617

Related:
https://landairsea.com/blog/how-accurate-are-gps-unit-coordinates-really/
> Depending on your device’s GPS technology, though, you could get accuracy anywhere from a millimeter to about five meters

## Unicode conversion
From the Notes section of the [ImageInfo documentation](https://exiftool.org/ExifTool.html#ImageInfo):
ExifTool returns all values as byte strings of encoded characters. Perl wide characters are not used.
Try this to use Perl wide characters:
`exiftool -v -P in.mp4 "-Keyword<${Keyword; use Encode; $_=decode('utf8',$_); s/(\w+)/\u\L$1/ug; $_=encode('utf8',$_)}"`
Note that it isn't strictly necessary to convert back to a byte string afterwards as I have done (since ExifTool should do this), but it is better safe than sorry.
https://exiftool.org/forum/index.php?msg=76987

## URIs are not links
https://exiftool.org/forum/index.php?msg=48058

## Using `find` (or Windows `Everything` search) to pass filesnames to exiftool
Note, exiftool's powerful built in batch ability means this should rarely be needed, but linux users might find this easier
https://exiftool.org/forum/index.php?msg=70887

On Windows, if you have [Everything Search](https://www.voidtools.com/), you can use its command line program `es` in the same way. Example, matching all jpegs with "Saturday" in the filename
`es files: saturday ext:jpg;jpeg | exiftool -@ - <rest of command>`

## Using `Geolocate`
The `-geolocate=geotag` feature is used if you are geotagging from a GPS track log. If the file already contains GPS, probably you should use `"-geolocate<gpsposition"`

## Using `Userparam` on the command line to fill multiple tags
You can use the `UserParam` api option to fill a variable and then use that variable to fill other tags.  This can help avoid mistyping.

`exiftool -userparam myvar="New Title" "-title<$myvar" "-comment<$myvar" a.jpg`

https://exiftool.org/forum/index.php?msg=45237

### iPhone 14 DNG writes XMP in non-standard place
https://exiftool.org/forum/index.php?msg=76645

## Using a shortcut to rename with multiple tags, while not throwing an error for missing ones
Revisit this and see if it can be condensed
https://exiftool.org/forum/index.php?msg=42949

## Using the [`-api NoDups` option](https://exiftool.org/ExifTool.html#NoDups)

Use the [`-TagsFromFile` option](https://exiftool.org/exiftool_pod.html#tagsFromFile-SRCFILE-or-FMT) to copy the tag back into the file, then add new list items with just the equal sign. If adding a list item from another tag, use a leading `-+` instead of a simple `-`

```
C:\>exiftool -G1 -a -s -subject y:\!temp\Test4.jpg -sep ##
[XMP-dc]        Subject                         : One##Two##Three##One##Two##Three##One##Two##Three##One##Two##Three##Five##One##Two##Three##Five##Five

C:\>exiftool -P -overwrite_original -api NoDups -TagsFromFile @ -subject -subject=One -subject=Two -subject=Three -subject=Three "-+Subject<Description" y:\!temp\Test4.jpg
    1 image files updated

C:\>exiftool -G1 -a -s -subject y:\!temp\Test4.jpg -sep ##
[XMP-dc]        Subject                         : One##Two##Three##Five
```

## Version and checksum locations
The current exiftool version can be found here
http://exiftool.org/ver.txt
Checksums for exiftool files can be found here
https://exiftool.org/checksums.txt

## Video GPS tracks different in different models from Garmin
> I was just looking at a Garmin DriveAssist 50 MP4 file. It is stupid, but the DriveAssist 50 stores GPS in an entirely different format from the DriveAssist 51

https://exiftool.org/forum/index.php?msg=75221

## Video time stamps not deleted with with `-All=`
Tags which are required and cannot be deleted, such as many Quicktime date/time tags, will not be removed with `-All=`. Sometimes they can be cleared. An example for the video timestamps would be to use `-Time:All=`
https://exiftool.org/forum/index.php?msg=54897

## When extracting a GPS track from a video, the resulting file repeatedly displays `gpx.fmt`.
https://exiftool.org/forum/index.php?msg=78475

## Why `LargeFileSupport` isn't on by default
https://exiftool.org/forum/index.php?msg=64263
To be changed in 12.88
https://exiftool.org/forum/index.php?msg=86920

## Why exiftool doesn't write GeoTiff tags
https://exiftool.org/forum/index.php?msg=12451

## Write to multiple tags at the same time using a wildcard or a shortcut.
https://exiftool.org/forum/index.php?msg=75792

## XMP data maximum size
https://exiftool.org/forum/index.php?msg=48877

