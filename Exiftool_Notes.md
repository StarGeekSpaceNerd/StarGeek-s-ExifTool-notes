StarGeek's exiftool notes  
===  
These are my unsorted notes and links to various use exiftool posts. Any suggestions on formatting/grouping these is welcome.  

# 1 Working with the ExifTool forums  
Notes on working with the forums

## How to add images to a post  
To inline an image, you would use the BBCode `[img]`/`[/img]` tags and place a link to the image in between  
Example:  
`[img]https://i.imgur.com/V2yCBli.png[/img]`  
If you are using Imgur, make sure you use the "Direct Link" URL, not the "Image Link" url.  

To Upload your own image, see this post  
https://exiftool.org/forum/index.php?msg=87312  

If the image is very wide/tall, then you can modify how the image is displayed like this to reduce the width  
`[img width=300]https://i.imgur.com/V2yCBli.png[/img]`  
or the height  
`[img height=300]https://i.imgur.com/V2yCBli.png[/img]`  
The image itself is unaffected and one posted, can be viewed in the original size by clicking on it.  

If the file is too large to add to the forums, you can use a file hosting site like Google Drive, DropBox, Mega.nz, etc and create a share link to the file. If you are using Google Drive, make sure the link is set to "Anyone with a link" instead of "Restricted". See [this post](https://exiftool.org/forum/index.php?msg=92921).  

# 2 Metadata  
Notes on metadata  
## ACDSee regions and sample image  
Sample image with ACDSee regions  
https://exiftool.org/forum/index.php?msg=57132  

## Apple doesn't understand metadata  
Links showing times when Apple incorrectly deals with metadata  
To do, dig up links on this  

### Apple Photo creates non-standard GPS reference tags in XMP  
Find links  

### Apple Photos Quicktime Timezone error  
Wildly inaccurate date/time in Apple Photos with date/time Time stamps missing time zone  
https://exiftool.org/forum/index.php?msg=56769  
with images  
https://exiftool.org/forum/index.php?msg=64363  

## Copy of the Metadata Working Group  _Guidelines for Handling Image Metadata_  
A copy of the Metadata Working Group PDF  
https://exiftool.org/forum/index.php?msg=53039  
Additionally, via Archive.org  
https://web.archive.org/web/20180919181934/http://www.metadataworkinggroup.org/pdf/mwg_guidance.pdf  

## Family History Metadata Working Group (FHMWG)  
A standard for dealing with family history. For the most part, it copies other standards such as the MWG and IPTC standards  
Main page  
https://github.com/fhmwg/current-tags  
Tag definitions  
https://github.com/fhmwg/current-tags/blob/stage2-essentials/stage2-essentials-overview.md  

## JPEG Snoop page with visuals on EXIF orientation  
Oritinal page was taken down, link via Archive.org  
https://web.archive.org/web/20180819022932/https://www.impulseadventure.com/photo/exif-orientation.html  

## Maker note tags documentation  
> Maker note tags are reverse engineered by camera owners since there is no official documentation available (with rare exceptions).  

https://exiftool.org/forum/index.php?msg=78692  

## Opinion on Dashcam manufacturers obfuscating the embedded data such as GPS tracks  
https://exiftool.org/forum/index.php?msg=76061  

## PNG chunk name capitalization rules  
https://exiftool.org/forum/index.php?msg=89213  

## XMP data maximum size  
https://exiftool.org/forum/index.php?msg=48877  

# 3 Best Practices  
Things that in my opinion, are the best way for dealing with metadata. Might separate this into a new file and use the full contents instead of just linking to forum posts.  

## Common Mistake #3
[Common Mistake #3, "Over-scripting"](https://exiftool.org/mistakes.html#M3) says that you shouldn't run exiftool in a loop, running it once for each file. Exiftool's startup time is the biggest performance hit, and doing so will greatly increase processing time.

As an example, in [this post](https://exiftool.org/forum/index.php?msg=92142), when the user looped exiftool, the process took ten minutes. After changing to use [PyExiftool](https://github.com/sylikc/pyexiftool), which uses the [`-stay_open` option](https://exiftool.org/exiftool_pod.html#stay_open-FLAG) and keeps exiftool running in the background, the processing time dropped to 30 seconds.

## Keep it (tag names) simple  
When writing tags, use only the tag name, adding the group 0 name (XMP: IPTC: EXIF:) only if necessary to avoid collisions, such as XMP:Headline vs IPTC:Headline.  Use the group 1 names only if absolutely necessary.  And about the only time that is necessary is if you are trying to write a tag that is marked as Avoid.  

Writing to group 1 specific locations without a deep understanding of the metadata can lead to writing to incorrect locations.  As an example, for some reason Sony didn't properly read the EXIF specs and some Sony cameras write the `ModifyDate` tag to the incorrect location (`IFD1` instead of `IFD0`).  And unless you knew beforehand that this was incorrect, it would lead you to thinking that `IFD1` was the correct location.  If you didn't include the specific group, exiftool would by default write to the correct location.  

Additionally, using only the base name will allow exiftool to update all tags with that name. If your command is something like  
`"-EXIF:ModifyDate=2025:01:01 12:00:00"`
you are **only** writing the `EXIF:ModifyDate`. Any other `ModifyDate` such as the `XMP:ModifyDate` will not be updated.

https://exiftool.org/forum/index.php?msg=80202  

# 4 External  
## Does the MWG (Metadata Working Group) still exist  
Answer, probably not anymore  
Still exists 2019  
https://exiftool.org/forum/index.php?msg=52224  
Still no change 2020  
https://exiftool.org/forum/index.php?msg=58151  

## Flickr uses Exiftool  
https://code.flickr.net/2012/06/01/parsing-exif-client-side-using-javascript-2/  

## Phil's EBird page  
https://exiftool.org/forum/index.php?msg=59975  
https://media.ebird.org/catalog?userId=USER1671030&mediaType=photo  

## Phil's ICAT Image Cataloging Tool  
https://exiftool.org/icat/  

# 5 Historical
## "Lost" ebv4linux interview with Phil  
In German, can be translated with web browser translation abilities  
https://web.archive.org/web/20150419003745/http://www.ebv4linux.de/modules.php?name=News&file=article&sid=26  

Technically not lost, because there's [a link](https://exiftool.org/#other_links) and a PDF with translation on the main exiftool page, but I found this while doing a deep dive into the forums.

## Tom Christiansen (co-author of "Programming Perl") and dealing with UTF-8  
https://exiftool.org/forum/index.php?msg=7642  

# 6 Unsorted notes  

## A discussion on deleting metadata  
https://exiftool.org/forum/index.php?msg=76627  

## Access another tag from within advanced formatting (correct)  
To access a different tag from within an advanced formatting, you would use this, replacing `tag` with the name of the tag (case-sensitive) you are accessing.   
`$self->GetValue('tag')`

To access a `UserParam` you would use this. `MYPARAM` is case insensitive.
`$self->Options('UserParam','MYPARAM')`

## Access another tag from within advanced formatting (incorrect)  
This way should not be used, Needs rewriting.  Instead, `$self->GetValue('tag')` should be used  
https://exiftool.org/forum/index.php?msg=34104  
`$$self{VALUE}{TAG}`  
For example, to remove Make from within the Model tag  
`exiftool "-title<${Model;s/\\\\s\\\*$$self{VALUE}{Make}\\\\s\\\*//i}" -m`  
This uses ExifTool internals feature to access the Make tag from within the advanced formatting expression for Model.  But a disadvantage of doing it this way is that you will get a warning due to an uninitialized value in this expression if Make doesn't exist, hence the -m option. The tag is case-sensitive.  
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

## Changing extension to Title Case  
This will upper case the first letter, then lower case the rest  
`-Filename=%f.%1ue%.1le`  
This can also be done with RegEx.  
`${Filename;s/(?<=\.)(\w)(\w+)$/\u$1\L$2/}`  
The first option would probably be slightly faster, but if you were doing other edits to the filename extension, then the RegEx would be necessary. For example, I prefer to have a extension of `.Jpg` over `.Jpeg`. This command will change `.jpeg` into `.jpeg`  
`exiftool "-Filename<${Filename;s/(?<=\.)jpeg$/jpg/i;s/(?<=\.)(\w)(\w+)$/\u$1\L$2/;} /path/to/files/`  

## Checking to see if a specific number of tags exists
This command checks several tags to see if they exist and increments a variable if they do. If a certain number of these tags do exist, then the `-if` option registers as `true` and the command continues.  
https://exiftool.org/forum/index.php?msg=71626

## config files and user-defined tags  
See the [[User defined tags index]]  

## Converting a local time to UTC  
Needs expansion and rewrite with the standard exiftool routines  
Requires that the `OffsetTime*` tag is set  
`${SubSecDateTimeOriginal#;use POSIX qw(strftime);DateFmt('%s');$_=strftime('%Y-%m-%d_%H-%M-%S',gmtime($_))}`  
https://exiftool.org/forum/index.php?msg=79228  

## Copy metadata from one file to another with completely different names using hardlinks to sync them  
A multistep operation to copy tags from one directory to another where the files have all been renamed and cannot be linked by editing the name, but can be linked by a tag, in this case `Duration`. This procedure creates hard links with names based upon `Duration` and allows copying the data based upon that.  
https://exiftool.org/forum/index.php?msg=68166  

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

## Don't use PDF:Keywords with commas  
https://exiftool.org/forum/index.php?msg=80503  

## Example color changes when removing ICC_Profile and Adobe APP14  
The JPEG APP14 Adobe segment contains some color information that may severely affect the image appearance if deleted.  
https://exiftool.org/forum/index.php?msg=32114  
Removing the ICC_Profile will change the colors, but the result will be a more subtle change  
https://exiftool.org/forum/index.php?msg=68249  

## EXIF in MOV/MP4 files is non-standard  
EXIF data is non-standard in files and will be lost if the file is edited. The best workaround would be to use the [`exif2xmp.args` file](https://github.com/exiftool/exiftool/blob/master/arg_files/exif2xmp.args) to copy the data to the corresponding tags in XMP  
https://exiftool.org/forum/index.php?msg=56282  

## Exiftool calculates `Duration` Incorrectly  
Exiftool calculates the `Duration` based upon the header metadata and doesn't analyze the stream itself.  If the header has incorrect data, then the value could be off. To get the exact duration requires the use of a video specific program like `ffmpeg`/`ffprobe`.  
https://github.com/exiftool/exiftool/issues/160#issuecomment-1293946184  

## Exiftool cannot write XMP qualifiers  
https://exiftool.org/forum/index.php?msg=62262  
https://exiftool.org/forum/index.php?msg=82245  

## Exiftool Group tag names  
The group names can be found under the  
`GetGroup` function or using -listg  
https://exiftool.org/ExifTool.html#GetAllGroups  

## Exiftool is slow reading PDF metadata
If exiftool is slow to read PDF metadata, it is likely that the PDF has been encrypted. If the PDF can be read without entering a password, it is a no password encrypted PDF. Why such a thing exists is beyond me.

The problem is because an external library to decrypt it could not be found, so the decryption code had to be done is pure Perl. See [this post](https://exiftool.org/forum/index.php?msg=24161).

A no password encrypted PDF can be decrypted with `qpdf`, as shown in [this post](https://exiftool.org/forum/index.php?msg=87766) in the same thread.

## Exiftool is slower when writing PNG files  
https://exiftool.org/forum/index.php?msg=89587  

## Exiftool JSON output, numerics strings output as numbers  
Example, if the `ExifToolVersion` has a trailing zero, it is output as numeric and the trailing zero may dropped by programs that treat it as a numeric value. This can be changed by setting the [`-api StructFormat` option](https://exiftool.org/ExifTool.html#StructFormat) to `JSONQ`  
```  
$ exiftool -J -ExifToolVersion test.heic  
[{  
  "SourceFile": "test.heic",  
  "ExifToolVersion": 12.60  
}]  
```  
https://github.com/exiftool/exiftool/issues/262  

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

## Extracted FLIR thermal images are strange  
From the docs on [FLIR RawData tags](https://exiftool.org/TagNames/FLIR.html#RawData)  
> Note that most FLIR cameras using the PNG format seem to write the 16-bit raw image data in the wrong byte order.  

This is what an extracted image looks like when the image data is in the wrong byte order  
![1-FLIR_RawThermalImage_Incorrect_Byte_Order.png](Images\1-FLIR_RawThermalImage_Incorrect_Byte_Order.png)  
The corrected image looks like this  
![2-FLIR_RawThermalImage_Corrected_Byte_Order.png](Images\2-FLIR_RawThermalImage_Corrected_Byte_Order.png)  

https://exiftool.org/forum/index.php?msg=91196  
https://exiftool.org/forum/index.php?msg=24992  
https://exiftool.org/forum/index.php?msg=72222  
Thanks to @thurston on the exiftool forum for the images  

## Extracting GPS data from MP4 video  
Original megathread  
https://exiftool.org/forum/index.php?msg=45447  
Otherwise now documented under [Inverse Geotagging](https://exiftool.org/geotag.html#Inverse)  

## Find all images within X distance of GPS Coordinates  
https://exiftool.org/forum/index.php?msg=59031  

## Fixed formatted tags  
An incomplete list of tags that would require overriding in order to write non-standard data. See this post  
https://exiftool.org/forum/index.php?msg=76643  
- `XMP-exif:GPSLatitude`  
- `XMP-exif:GPSLongitude`  

## garbage at end of string in strptime  
Not useful? Delete?  
https://exiftool.org/forum/index.php?msg=63144  

## Generate a user-defined tag only if requested  
https://exiftool.org/forum/index.php?msg=64462  

## Google GPS precision in videos  
Google Photos will not read GPS Latitude/Longitude with a precision of more than five decimals and an Altitude of more than four decimals.  
 https://exiftool.org/forum/index.php?msg=87423  

## Google Photos changed Description to Other
Around January 2022, Google stopped copying the `XMP:Description`/`IPTC:Caption-Abstract` to their "Description" property and instead copied it to the "Other" property.
https://exiftool.org/forum/index.php?msg=71217

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
The problem is that there really isn't a standard for embedding a GPS track in a video\* Currently, exiftool reads \*\*77 different ways\*\* that a GPS track can be in a video and there are about half a dozen more in which the format hasn't been decoded. I have yet to find a program that will embed a GPS track into a video file.  
And that won't be the only data you will lose when recompressing a video. The same situation exists with the EXIF data that is written into the video. Most video data is \[url=https://exiftool.org/TagNames/QuickTime.html\]Quicktime data\[/url\] and EXIF data in a video file is non-standard. But camera companies shove it in there anyway, with each company doing it in different ways.  
The best you can do is extract the GPS data into a GPX track and copy the EXIF data into the corresponding XMP tags (see the [url=https://github.com/exiftool/exiftool/blob/master/arg_files/exif2xmp.args]\[tt\]exif2xmp.args\[/tt\] file\[/url\] on GitHub), which are allowed in a video file.  
\*Technically, there is a standard by Google, but nobody follows it, and I've never found any software that write this format. I mention it in [url=https://exiftool.org/forum/index.php?msg=69582]this Exiftool forum's post\[/url\], which has a response from the author of exiftool  

## GPS reference directions  
Contains GIF of how to copy/paste GPS coordinates in a spreadsheet in order to create the Ref direction tags as well  
https://exiftool.org/forum/index.php?msg=73550  

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

## iPhone 14 DNG writes XMP in non-standard place  
https://exiftool.org/forum/index.php?msg=76645  

## IPTCDigest - IPTCDigest is not current  
https://exiftool.org/forum/index.php?msg=75864  

## jonkeren's Exiftool Commands/cheat sheet  
One exiftool user's cheat sheet  
Some of these can be simplified or updated  
https://github.com/jonkeren/Exiftool-Commands  

## JSON output and numbers  
> The values output by exiftool are not typed, which leads to problems when converting for the JSON output. If it looks like a number, then ExifTool writes a JSON number, otherwise it quotes it as a string.  
https://exiftool.org/forum/index.php?msg=37780  

## Keeping alt-lang tags when updating  
https://exiftool.org/forum/index.php?msg=60655  

## List type tags: Example of how list type tags are separated/EXIF time stamps breakdown  
https://exiftool.org/forum/index.php?msg=76017  

## List type tags: What are List Type tags?  
List type tags are tags which are saved in the file as individual separate entries.  While many programs will display them as comma/semicolon separated, they are not.  Each entry is completely self contained and separate from the others.  An example of this can be easily seen by looking at the raw data in the file.  Here's what it looks like in  the `XMP-dc:Subject`  tag  
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
![Bridge-2023-01-15_09.35.14.png](Images\Bridge-2023-01-15_09.35.14.png)  

## Looking at the details of a file  
Examples of `-v` and `-htmldump` options  
https://exiftool.org/forum/index.php?msg=74866  

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

## Phil's script to replace jpeg image without changing metadata  
Phil uses this `swap_image` script to remove images from the [ExifTool Meta Information Repository](https://exiftool.org/sample_images.html)  
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

## PowerShell requires decimal values to be quoted  
No link ATM, but if a decimal value isn't quoted, then it is separated at the decimal point and the rest is treated as if it were a separate parameter. The PS highlighting indicates the separation.  
Example:  
`PS C:\> exiftool -P -overwrite_original -Description=9.9 y:\!temp\Test4.jpg  
Error: File not found - .9  
    1 image files updated  
    1 files weren't updated due to errors  
PS C:\> exiftool -G1 -a -s -Description y:\!temp\Test4.jpg  
[XMP-dc]        Description                     : 9`  

## PowerShell sucks at quoting  
https://exiftool.org/forum/index.php?msg=80581  
Use backticks and double all interior single quotes
https://exiftool.org/forum/index.php?msg=77722  
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_quoting_rules?view=powershell-7.3  

## Quicktime delete date/time timestamps  
https://exiftool.org/forum/index.php?msg=54897  

## Remove all metadata from a video  
There is some metadata in video files that exiftool can't remove, usually non-standard additions to the file. Examples of this are GPS tracks and EXIF data. Because there isn't a standard for this type of metadata in a video, every company writes the data in different ways, sometimes differing between camera models (add link to Go Pro example here).  

The program [AVIDemux](https://avidemux.sourceforge.net/) is a [FOSS](https://en.wikipedia.org/wiki/Free_and_open-source_software) program that doesn't copy any metadata, so it can be used to remove all the metadata from a video file. Despite its name, it can edit MP4, MOV, and MKV files. This forum posts shows the settings I use to remove metadata in a lossless manner.  
https://exiftool.org/forum/index.php?msg=64673  

`ffmpeg` can also be used losslessly remove metadata. This is the command I use.  
`ffmpeg -hide_banner -i input.mp4 -c copy -map 0 -map_metadata -1 output.mp4`  

## Renaming files and XMP sidecars  
https://exiftool.org/forum/index.php?msg=6201  

## Running exiftool on a JSON file returns incorrect data  
This happens when the command in FAQ \#3 isn't used. For example, in this sequence of commands, the `MimeType` of a JPEG is saved to a JSON file. When listed, the `MimeType` for the JSON file is reported as `image/jpeg`, not as `application/json`. The command in FAQ \#3 is requrired to see that there is the `MimeType` of the JSON file and the `MimeType` embedded in the JSON file.  
```  
C:\>exiftool -MimeType -j y:\!temp\Test4.jpg  >temp.json  
C:\>exiftool -MimeType Temp.json  
MIME Type                       : image/jpeg  
C:\>exiftool -G1 -a -s -MimeType Temp.json  
[File]          MIMEType                        : application/json  
[JSON]          MIMEType                        : image/jpeg  
```  

## Set `.exiftool_config` to always show unknown tags  
Example use of using different default [Options](https://exiftool.org/ExifTool.html#Options). Setting `LargeFileSupport` in this way is a common use.  
https://exiftool.org/forum/index.php?msg=79956  

## Setting `AllDates` from filenames that have incomplete date/times  
If only the Year or YearMonth for a file is known and in the filename, this command will default to 01 month and 01 day, as well as 00:00:00 for the time when copying time stamp from the filename.  
https://exiftool.org/forum/index.php?msg=76082  

## Setting notifications on the forum  
https://exiftool.org/forum/index.php?msg=87615  

## "Shifting" non-shiftable composite date/time tags  
Composite date/time tags such `SubSecDateTimeOriginal` are not shiftable by using `-=`/`+=`.  To work around, use the `ShiftTime` helper function  
`"-SubSecDateTimeOriginal<${SubSecDateTimeOriginal;ShiftTime('-0:0:10')"`  
https://exiftool.org/forum/index.php?msg=78691  

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
More complex Natural Order compare (i.e. the number 1 sorts before the number 10)  
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
Examples of how the StackOverflow Windows UTF8 option may affect GUIs and fonts  
https://exiftool.org/forum/index.php?msg=72233  
It also affects ISO-8859-1 (extended ASCII) characters   
https://www.youtube.com/watch?v=QFAyxoGTgGE

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

## `-TagsFromFile` and `-All:All` / `-All`  
Working out the difference between various `-GROUP:All` tag copies  
https://exiftool.org/forum/index.php?msg=79962  

## To do, explain why there may be differences in GPS Coordinate written compared to what is read, and why the EXIF GPS coordinates may be different than the XMP ones. Also, Accuracy of decimal places/how many decimals are too many  
Need to consolidate and simplify these  
Early post on differences  
https://exiftool.org/forum/index.php?msg=7617  
Related:  
https://landairsea.com/blog/how-accurate-are-gps-unit-coordinates-really/  
> Depending on your device’s GPS technology, though, you could get accuracy anywhere from a millimeter to about five meters  

## "Undocumented" subroutines  
Technically documented in the source code, but theses aren't really documented outside of that.  
These can be found in `ExifTool.pm`  
- TimeZoneString  
- ConvertUnixTime  
- GetUnixTime  
Post to refer to with regards to figuring out time zone  

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

## Why exiftool doesn't write GeoTiff tags  
https://exiftool.org/forum/index.php?msg=12451  

## Windows unable to display metadata and thumbnail from a video  
Windows will chock and stop displaying metadata in the Properties window if there is too much metadata

If the file contains the Apple `FullFrameRatePlaybackIntent` tag, then it will not display a thumbnail or any metadata.  
https://exiftool.org/forum/index.php?msg=90410  

## Write to multiple tags at the same time using a wildcard or a shortcut.  
https://exiftool.org/forum/index.php?msg=75792  

## Write to multiple tags at the same time using using the `Userparam` option  
You can use the `UserParam` api option to fill a variable and then use that variable to fill other tags.  This can help avoid mistyping.  
`exiftool -userparam myvar="New Title" "-title<$myvar" "-comment<$myvar" a.jpg`  
https://exiftool.org/forum/index.php?msg=45237  

## Writing GPS track files without redirection  
Commands to write GPS tracks using the [`-w` (`-TextOut`) option](https://exiftool.org/exiftool_pod.html#w-EXT-or-FMT--textOut)/[`-W` (`-TagOut`) option](https://exiftool.org/exiftool_pod.html#W-FMT--tagOut) instead of command line redirection  
https://exiftool.org/forum/index.php?msg=78826  

# 7 Depricated  

## Parse H264 stream  
Edit the source code to activate steam parsing  
This is no longer needed. Using `-ee2` or higher activates it.  
https://exiftool.org/forum/index.php?msg=65183  

## Why `LargeFileSupport` isn't on by default  
https://exiftool.org/forum/index.php?msg=64263  
To be changed in 12.88  
https://exiftool.org/forum/index.php?msg=86920  

# 8 Threads needing further evaluation  

## Problem writing `FileCreateDate` when also writing video time stamps (Windows only?)  
https://exiftool.org/forum/index.php?msg=71755  
