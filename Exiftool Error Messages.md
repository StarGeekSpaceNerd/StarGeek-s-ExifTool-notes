Exiftool Error Messages 
=== 
Incomplete notes on various warnings and errors issued by exiftool. In some cases, it will be a standard copy/paste response for the forum, such as with `IPTCDigest`

This is very much a work in progress

# 1 Warning: \[minor\]
Needs definition and how it compares to other warnings
## Possibly incorrect maker notes offsets/Adjusted MakerNotes base by
Very old post which has breakdown of problem  
https://exiftool.org/forum/index.php?msg=6993

## Tag 'XMP:CreateDate' not defined

## Warning: \[Minor\] Not decoding some large array(s). Ignore minor errors to decode

Some tags have a large amount of data and often it is not very useful except to the program that wrote it. As decoding such large arrays take longer to process, exiftool will limit the output unless the [`-m` (`-ignoreMinorErrors`) option](https://exiftool.org/exiftool_pod.html#m--ignoreMinorErrors) is used.f  
https://exiftool.org/forum/index.php?msg=69788f

# 2 Warning
Needs definition and how it compares to other warnings
## Bad length ICC_Profile  
to do
## Bad offset for <TAG>
This is usually in regards to EXIF (maybe IPTC) tags. It means that some program has incorrectly written the EXIF block.

A targeted, possible fix (I haven't tested it, no samples) would be to remove that tag and re-add it.
`exiftool -TAG= -TagsFromFile @ -TAG /path/to/files/`

A more shotgun approach is detailed in [FAQ #20](https://exiftool.org/faq.html#Q20). **WARNING:** Never used the command listed in FAQ #20 on RAW file types such as NEF, CR2, ARW, etc.

## Duplicate <TAG> tag in <GROUP>
This means that some program has incorrectly written a multiple copies of TAG. The first thing to do is check to see if the tags are different and if they are, decide which is correct  
`exiftool -G1 -a -s -TAG file.jpg`  

Sometimes, the extra tags are written in the wrong group, expecially if they are EXIF tags. In these cases, you may have to explicitly delete the extra tags by including the group they are in. For example, if there was an `Orientation` tag in `IFD1` (it normally appears in `IFD0`) , you would have 

## Error converting date/time for
to do

## Fixed incorrect URI for xmlns:MicrosoftPhoto
At some point, Microsoft changed how they wrote the URI in Microsoft XMP tags, which is something they shouldn't have done. The difference is simply an extra slash.  I believe it originally was
`xmlns:MicrosoftPhoto='http://ns.microsoft.com/photo/1.0/'`
and then Microsoft changed it to
`xmlns:MicrosoftPhoto='http://ns.microsoft.com/photo/1.0'`

The "Fixed" message indicates it was fixed upon reading the data. It will not actually be fixed unless the `Xmp-Microsoft` group is rewritten. This can be done by rewriting any of the tags in the group, such as `LastKeywordXMP`, or rewriting the entire group, e.g. 
`-XMP-microsoft:all= -TagsFromFile @ -XMP-microsoft:all`

Generally, this warning can be ignored. It hasn't been shown to cause any problems in any software to date.

Phil's comment on the subject
[https://exiftool.org/forum/index.php?msg=37095](https://exiftool.org/forum/index.php?msg=37095)

## ICC_Profile deleted. Image colors may be affected

Removing the `ICC_Profile` will impact the colors on viewers that read the profile. This can happen when using a command such as  
`exiftool -All= /path/to/files/`  
In order to keep the profile, the [`-TagsFromFile` option](https://exiftool.org/exiftool_pod.html#tagsFromFile-SRCFILE-or-FMT) must be used to recover the data  
`exiftool -All= -TagsFromFile @ -ICC_Profile /path/to/files/`

## Invalid EXIF text encoding for &lt;TAG&gt;
https://exiftool.org/forum/index.php?msg=69733

## Invalid time string () when shifting TimeCreated
to do

## IPTCDigest is not current. XMP may be out of sync
https://exiftool.org/forum/index.php?msg=75864

## No writable tags set from ?
This means exactly what it says. You are attempting to copy tags that do not exist in the source file. Use the command in [FAQ #3](https://exiftool.org/faq.html#Q3) to see what tags are actually available.

## Warning: Unknown file type
to do

## Wrong IFD for
to do

# 3 Error
Needs definition and how it compares to other warnings
## Bad format (###) for (ExifIFD|IFD0|IFD1) entry ###
This indcates a corrupted EXIF block and at least one, if not more, EXIF tags have been lost. The command in [FAQ #20](https://exiftool.org/faq.html#Q20) may help repair the file but make sure you have a backup and do **not** use the command on RAW file types.

## Bad Photoshop IRB resource

may also be a warning

## File not found <NameOfTag>

This usually means you have a quoting problem or are forgetting the leading hyphen in a tag name. What is happening is that because of the improper quotes or missing hyphen, exiftool is getting the tag name without being told it is a tag name. As a result, it appears to be the name of a file, resulting in this error.

Example, this indicates that `Description` did not have a leadiing hyphen    
`Error: File not found Description`

# 4 To do
Warnings that may need to be added
`Warning                         : [minor] Invalid CanonCameraSettings data
Warning                         : [minor] Invalid CanonShotInfo data
Warning                         : [minor] Invalid CanonAFInfo data
Warning                         : [minor] Non-standard ExifIFD tag 0xea1c Padding
Warning                         : [minor] Non-standard ExifIFD tag 0xea1d OffsetSchema
Warning                         : [minor] Non-standard IFD0 tag 0xea1c Padding
