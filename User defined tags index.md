User defined tags index
===
# 1 External User defined tags
These are user defined tags that must be called using the [`-Config` option](https://exiftool.org/exiftool_pod.html#config-CFGFILE) or by merging them into the `.ExifTool_config` file.

There are several extremely specific user defined tags in the forums, such as [this config](https://exiftool.org/forum/index.php?msg=75641), that have not been included here. These are usually not useful to anyone outside the person using them, though they can be useful as example code. They can be found by searching the forums for `"ExifTool::UserDefined"`.

## Quicktime Full-frame-rate-playback-intent tag
### 1 Description
### 2 Tags created  
`Keys:Full-frame-rate-playback-intent`  
### 3 Source
https://exiftool.org/forum/index.php?msg=90347

## GeoSetter XMP tag
### 1 Description
This tag is part of the `.exiftool_config ` file used by GeoSetter
### 2 Tags created  
`XMP-geosetter:ForeignKeys`
### 3 Source
Installed with the GeoSetter program. A copy appears in this post
https://exiftool.org/forum/index.php?msg=15197
### 4 Notes
The use is unknown.

## BioLifePro XMP tags
### 1 Description
Tags for the `XMP-BioLifePro` group.
### 2 Tags created  
`XMP-BioLifePro:BrandName`  
`XMP-BioLifePro:ExpirationDate`  
`XMP-BioLifePro:FacingIndicator`  
`XMP-BioLifePro:FileName`  
`XMP-BioLifePro:Gdti`  
`XMP-BioLifePro:Gtin`  
`XMP-BioLifePro:ProductName`  
`XMP-BioLifePro:ValidFromDate`  
### 3 Source
https://exiftool.org/forum/index.php?msg=66714
### 4 Notes
These appear to be tags created for private use.

## markdown Template
### 1 Description
Tags for the `XMP-levi` group
### 2 Tags created  
`XMP-levi:ColorName`  
`XMP-levi:ImageView`  
`XMP-levi:ProductCode`  
`XMP-levi:ProductName`  
### 3 Source
https://exiftool.org/forum/index.php?msg=27360  
### 4 Notes
These appear to be tags created for private use.  

## Android `XMP:FStop`
### 1 Description
The Android app "F-Stop" uses a "heart" icon that maps to a custom xmp tag.

### 2 Tags created
`XMP-fstop:favorite`

### 3 Source
https://exiftool.org/forum/index.php?msg=85484

## Aspect Ratio config
### 1 Description
Returns aspect ratio and image format (landscape/portrait/square) of image

### 2 Tags created
`Composite:AspectRatio`  
`Composite:ImageFormat`

### 3 Source
https://exiftool.org/forum/index.php?msg=84556

Replaces my own previous config  
https://exiftool.org/forum/index.php?msg=36847

## astronomy visualization metadata exiftool profile
### 1 Description
Write AVM tags in XMP format to a file using the Perl package Exiftool. The AVM standard currently supported is version 1.1.

### 2 Tags created
Many tags, ~39 in `XMP-avm` group

### 3 Source
Forum post  
https://exiftool.org/forum/index.php?msg=26531  
Config file on GitHub  
https://github.com/clr/astronomy_visualization_metadata_exiftool_profile

### 4 Notes
The standard looks like it's currently ver 1.2. Not known if there's an update for this config or not
**Astronomy Visualization Metadata Standard**
https://www.virtualastronomy.org/avm_metadata.php

## Combined Keywords
### 1 Description
Combines the `Subject`, `Keywords`, and `XPKeywords` tags, removes any duplicate entries, and returns the combined list.
### 2 Tags created
`Composite:CombineKeys`
### 3 Source
https://exiftool.org/forum/index.php?msg=67042
### 4 Notes
Probably obsolete with the addition of the [`-api NoDups` option](https://exiftool.org/ExifTool.html#NoDups).

## Config for buggy software that writes `XMP-iptcCore:Caption`
### 1 Description
There's no such thing as `XMP-iptcCore:Caption` tag, but some unknown software will write this. This tag will allow editing of this tag. Bare minimal config file

### 2 Tags created
`XMP-iptcCore:Caption`

### 3 Source
https://exiftool.org/forum/index.php?msg=75673

## Create QR code image from GPS coordinates
### 1 Description
Creates a QR code PNG image from the embedded GPS coordinates by running `qrencode` using the coordinates embedded in the file.

This example command will create a QR code PNG for every file in a directory with GPS coordinates. The base filename will have `-QR` appended to it.  
`exiftool -config GPSQRCode.config -GPSQRCode -b -W %d%f.png y:\!temp\Test4.jpg`
### 2 Tags created  
`Composite:GPSQRCode`
### 3 Source
https://exiftool.org/forum/index.php?msg=87698
### 4 Notes
Source  
https://github.com/fukuchi/libqrencode  
Windows Port  
https://sourceforge.net/projects/qrencode-for-windows/  
Tutorial  
https://www.howtogeek.com/devops/how-to-create-qr-codes-from-the-linux-command-line/

## DigiKam_Audio_Video_tags.config
### 1 Description
For use with `exiv2`/Digikam `XMP-audio`/`XMP-video` tags. Unfortunately, there are a **lot** of these tags and `exiv2` does not do any sanity checks on the data it is embedding, so there isn't a way to create a proper test file.

It's quite probable that some of these are broken, as there are some that are listed as "closed list", but without any details as to what that closed list is supposed to be.

### 2 Tags created
Extensive list, see config file or run this command with the config file  
`exiftool -config DigiKam_Audio_Video_tags.config -list -xmp-audio:all -list -xmp-video:all`

### 3 Source
Original post, GPS only tags  
https://exiftool.org/forum/index.php?topic=15228#msg81856

Full config file  
https://exiftool.org/forum/index.php?msg=87162

### 4 Notes
Links  
https://community.kde.org/GSoC/2012/Ideas#Project:_Video_metadata_support  
XMP-video source:  
https://github.com/Exiv2/exiv2/blob/06fe8268dcd2559f8039529c62ea6d97b1adebb3/src/properties.cpp#L3424  
XMP-audio source:  
https://github.com/Exiv2/exiv2/blob/06fe8268dcd2559f8039529c62ea6d97b1adebb3/src/properties.cpp#L3975  
Exiftool forum thread, especially the last post:  
https://exiftool.org/forum/index.php?msg=81852

## DirTree
### 1 Description
Creates list out of directory path.  
Example use, adding each directory level to the `Keywords` tag.  
Might be deprecated and possible to replace by inline code.

### 2 Tags created
`Composite:DirTree`

### 3 Source
https://exiftool.org/forum/index.php?msg=21444

## EarliestDate
### 1 Description
Similar to the `OldestDateTime` user defined tag, this tag also includes the name of the oldest tag.
### 2 Tags created
`Composite:EarliestDate`
### 3 Source
https://exiftool.org/forum/index.php?msg=83979
### 4 Notes
Also see OldestDateTime (make this into link)

## Esko XMP structured tags
### 1 Description
Esko XMP ink structure  
More info on this is needed

### 2 Tags created
#### 1 Structured tag
`XMP-egGr:Inks`

#### 2 Flattened Tags
`XMP-egGr:InksAngle`  
`XMP-egGr:InksAttribute`  
`XMP-egGr:InksB`  
`XMP-egGr:InksBook`  
`XMP-egGr:InksDotshape`  
`XMP-egGr:InksEgname`  
`XMP-egGr:InksFrequency`  
`XMP-egGr:InksG`  
`XMP-egGr:InksName`  
`XMP-egGr:InksPrintingmethod`  
`XMP-egGr:InksR`  
`XMP-egGr:InksType`

### 3 Source
http://exiftool.org/forum/index.php/topic=8082#msg41411

## excire.config
### 1 Description
Allows editing of a `XMP-excire` tags

### 2 Tags created
`XMP-excire:HierarchicalSubject`

### 3 Source
https://exiftool.org/forum/index.php?msg=72877

### 4 Notes
Unknown if there are other tags in the `XMP-excire` group

## FacesNotInKeywords 
### 1 Description
This tag reads the `Xmp-Microsoft:RegionPersonDisplayName` and compares it to the `Subject` and `Keywords` tags. Any region names that already exist in the `Subject`/`Keywords` tags are removed, leaving only a list of names that could then be added to the `Subject`/`Keywords` tags.

This can be adapted for other region types by changing `Require` tag.
### 2 Tags created  
`Composite:FacesNotInKeywords`
### 3 Source
https://exiftool.org/forum/index.php?msg=82479

## `GPS2MapUrl.config`
### 1 Description
Reads GPS coordinates in a file and creates an URL to various map websites
### 2 Tags created  
`Composite:GoogleMapsUrl`  
`Composite:BingMapsUrl`  
`Composite:OpenStreetMapsUrl`  
`Composite:MapquestMapsUrl`  
`Composite:YandexMapsUrl`  
### 3 Source
https://exiftool.org/forum/index.php?msg=51226  
https://github.com/StarGeekSpaceNerd/GPS2MapUrl.config  

## GPSDateTimeLocal
### 1 Description
Returns `GPSDateTime` converted to local time and time zone  
Convert to helper function?

### 2 Tags created
`Composite:GPSDateTimeLocal`

### 3 Source
https://exiftool.org/forum/index.php?msg=25011

### 4 Notes
This probably can be done inline now. Might move this to depricated

## Hayo Baan's XMP Sidecar GPS check
### 1 Description
Checks the file and any existing XMP sidecar to see if the GPS data exists. Returns the name of the file containing the data. Could be altered to check different tags. Maybe create helper function?

### 2 Tags created
`Composite:GPSIsSet`

### 3 Source
https://exiftool.org/forum/index.php?msg=40917

## ISAD(G)
### 1 Description
Needs more information

### 2 Tags created
`XMP-isadg` tags, unsure of exact names  
Multiple structures  
`XMP-isadg:Alliedmaterials`  
`XMP-isadg:Conditionsaccessuse`  
`XMP-isadg:Contentstructure`  
`XMP-isadg:Context`  
`XMP-isadg:Descriptioncontrol`  
`XMP-isadg:Identity`  
Standard tag  
`XMP-isadg:NotesNote`  

### 3 Source
https://exiftool.org/forum/index.php?msg=67187

### 4 Notes
Related link?  
https://web.archive.org/web/20231207063626/https://docs.museosabiertos.org/en/recursos/isadg

## join_tags.config
### 1 Description
Can be used to join KEY:VALUE paired tags. Originally for `AcquisitionRecordGroupName` and `AcquisitionRecordGroupValue` Sony tags but can be modified to work with other KEY:VALUE tags, such as MKV tags. (the latter use might be deprecated with newer versions)

### 2 Tags created
`Composite:JoinTags`

### 3 Source
https://exiftool.org/forum/index.php?msg=63788

### 4 Notes
There is a version of this to deal with MKV files  
https://exiftool.org/forum/index.php?msg=63802

## Jpeg Compression Ratio
### 1 Description
Generates a ratio of the uncompressed size to the compressed size of a jpeg

### 2 Tags created
`Composite:JPEGCompression`  
`Composite:JPEGBitsPerPixel`

### 3 Source
https://exiftool.org/forum/index.php?msg=52453

## LayerGroups.config
### 1 Description
More data needed

### 2 Tags created
#### 1 Structured tag
`XMP-ns:LayerGroups`

#### 2 Flattened Tags
`XMP-ns:LayerGroupsName`  
`XMP-ns:LayerGroupsFileSuffix`  
`XMP-ns:LayerGroupsName`  
`XMP-ns:LayerGroupsProfileName`  
`XMP-ns:LayerGroupsProfileOverride`  
`XMP-ns:LayerGroupsResizeOps`  
`XMP-ns:LayerGroupsXmlRawData`

### 3 Source
https://exiftool.org/forum/index.php?topic=6827#msg34159

## Microsoft Regions size percentage
### 1 Description
Calculates the percentage of image area allocated to each region

### 2 Tags created
`Composite:RegionPercentage`

### 3 Source
https://exiftool.org/forum/index.php?msg=55744

### 4 Notes
Only works on Microsoft regions.  
Possible to do: expand to other region types.  
Might be better to get the full structure, as I think this will fail on regions without a name

## MobileSheets sheet music reader tag
### 1 Description
Tags for use with PDFs used by the MobileSheets sheet music reader program
### 2 Tags created  
`XMP-pdfx:Album`  
`XMP-pdfx:Books`  
`XMP-pdfx:Duration`  
`XMP-pdfx:Key`  
`XMP-pdfx:Source`  
### 3 Source
https://exiftool.org/forum/index.php?msg=81215
### 4 Notes
The `XMP-pdfx` tag group is a catch all for application specific PDF tags. As such, they are not built into exiftool and a config file must be used to write them.  
See the [`XMP-pdfx](https://exiftool.org/TagNames/XMP.html#pdfx) page.

## MWGKeywordsConversion
### 1 Description
Converts MWG Keywords into `HierarchicalSubject` as well as the reverse  
Note, may not be accurate as I may have not correctly understood the standard

### 2 Tags created
`Composite:MWGKeywordsToHS`  
`Composite:HSToMWGKeywords`  

### 3 Source
https://exiftool.org/forum/index.php?msg=48355

### 4 Notes
Related link  
https://exiftool.org/forum/index.php?msg=47676

## My Timezone lookup
### 1 Description
Uses Google's TimeZone api to get time zone data for a specific city/country or GPS coordinates.  
Requires a Google TimeZone api key, which requires a billing account and will charge with after monthly credit is used  
See  
https://developers.google.com/maps/documentation/timezone/get-api-key

### 2 Tags created
`Composite:GoogleLookUpTimeZone`  
`Composite:GoogleLookUpTimeZoneDaylightSavings`  
`Composite:GoogleLookUpTimeZoneID`  
`Composite:GoogleLookUpTimeZoneName`  
`Composite:GoogleLookUpTimeZoneRaw`  

### 3 Source
https://exiftool.org/forum/index.php?msg=58904

## MyHS
### 1 Description
This tag will write to `HierarchicalSubject` and leaf keywords to `IPTC:Keywords` and `XMP:Subject`. It will only write `IPTC:Keywords` if IPTC data exists, which is the equivilent to using the [`-wm cw` (`-writeMode cw`) option](https://exiftool.org/exiftool_pod.html#wm-MODE--writeMode). 
### 2 Tags created  
`Composite:MyHS`
### 3 Source
https://exiftool.org/forum/index.php?msg=87735

## MyloEdit tags
### 1 Description
Config file to edit MyloEdit tags,

### 2 Tags created
`XMP-MY:DateRangeEnd`  
`XMP-MY:DateRangeScope`  
`XMP-MY:DateRangeStart`  
`XMP-MY:Flag`  
`XMP-MY:MetadataDate`  
`XMP-MY:ProcessVersion`  
`XMP-MY:Undated`

### 3 Source
https://exiftool.org/forum/index.php?msg=71122

## Nikon View NKSC config 1
### 1 Description
`viewnx.config`  
Reads data from Nikon NKSC sidecar files

### 2 Tags created
`XMP-Sdc:About`  
`XMP-Sdc:Version`  
`XMP-Sdc:Appversion`  
`XMP-Sdc:Appname`  
`GPS-Ast:About`  
`GPS-Ast:Version`  
`GPS-Ast:GPSVersionID`  
`GPS-Ast:GPSVersionIDType`  
`GPS-Ast:GPSLatitudeRef`  
`GPS-Ast:GPSLatitudeRefType`  
`GPS-Ast:GPSLatitude`  
`GPS-Ast:GPSLatitudeType`  
`GPS-Ast:GPSLongitudeRef`  
`GPS-Ast:GPSLongitudeRefType`  
`GPS-Ast:GPSLongitude`  
`GPS-Ast:GPSLongitudeType`  
`GPS-Ast:GPSMapDatum`  
`GPS-Ast:GPSMapDatumType`  
`XMP-Nine:About`  
`XMP-Nine:Version`  
`XMP-Nine:NineEdits`  
`XMP-Nine:Label`  
`XMP-Nine:Rating`  
`XMP-Nine:Trim`

### 3 Source
https://exiftool.org/forum/index.php?msg=52393

## Nikon View NKSC config 2
### 1 Description
A newer version of the previous?

### 2 Tags created
Need to take time to figure out the differences between this and the other version

### 3 Source
https://exiftool.org/forum/index.php?msg=52458

## Northrup Image Standard Config
### 1 Description
Tony Northrup's idea of an image setting standard

### 2 Tags created
Shortcut Tags  
`NorthrupSC` Contains  

- `Aperture`  
- `ShutterSpeed`  
- `FocalLength`  
- `ISO`  
- `POV`  
- `ScaleFactor35efl`  

`PrintSize` Contains  

- `NativeImageSize`  
- `PhysicalImageSizeB`  

Composite Tags
`Composite:NativeImageSize`  
`Composite:Northrup35`  
`Composite:NorthrupAuto1`  
`Composite:PhysicalImageSizeB`

### 3 Source
https://exiftool.org/forum/index.php?msg=60098  
Youtube source, "Camera settings are outdated. Here's a better way. WARNING: NERDY"  
https://www.youtube.com/watch?v=OxOZoWtNJuo

## Number of tags in a file
### 1 Description
Returns the number of tags exiftool found for a file
### 2 Tags created  
`Composite:CountTags`
### 3 Source
https://exiftool.org/forum/index.php?msg=71227
### 4 Notes
I haven't checked, but this most likely will count flattened tags in addition to the base structered tag. It probably will not count tags that are not normally extracted unless requested, such as the Mac `XAtt*`/`MDItem*` tags.

## OldestDateTime
### 1 Description
Returns oldest Date/time stamp out of multiple common tags.

### 2 Tags created
`Composite:OldestDateTime`

### 3 Source
https://exiftool.org/forum/index.php?msg=40757

Requires PrintConv patch as listed in this post  
https://exiftool.org/forum/index.php?msg=43926

### 4 Notes
Also see EarliestDate (make this into link)

## PDF bookmark count
### 1 Description
Returns the number of bookmarked pages in a PDF
### 2 Tags created  
`UserDefined:NumOutlines`
### 3 Source
https://exiftool.org/forum/index.php?msg=79450
### 4 Notes
To do, some PDFs will return a `NumOutlines` value of 0 and do not have any bookmarks when the file is opened. A check needs to be added to ignore a value of 0.

## PhaseOne aerialgps namespace
### 1 Description
Tags for `XMP-aerialgps` namespace

### 2 Tags created
`XMP-aerialgps:GPSAltitudeAccuracy`  
`XMP-aerialgps:GPSEventID`  
`XMP-aerialgps:GPSFlightAltitude`  
`XMP-aerialgps:GPSFlightAltitudeRef`  
`XMP-aerialgps:GPSFlightLatitude`  
`XMP-aerialgps:GPSFlightLongitude`  
`XMP-aerialgps:GPSIMUFlightPitch`  
`XMP-aerialgps:GPSIMUFlightRoll`  
`XMP-aerialgps:GPSIMUFlightYaw`  
`XMP-aerialgps:GPSIMUFlightYawRef`  
`XMP-aerialgps:GPSIMUPitch`  
`XMP-aerialgps:GPSIMURoll`  
`XMP-aerialgps:GPSIMUYaw`  
`XMP-aerialgps:GPSIMUYawRef`  
`XMP-aerialgps:GPSLatitudeAccuracy`  
`XMP-aerialgps:GPSLongitudeAccuracy`  
`XMP-aerialgps:GPSRelativeAltitude`

### 3 Source
Original  
https://exiftool.org/forum/index.php?msg=75396  
Current   
https://exiftool.org/forum/index.php?msg=77952  

### 4 Notes
This is a good config to reference when creating GPS type tags

## Photoshop group tags

### 1 Description
Tags within the `Photoshop` group. Not very useful under most circumstances

### 2 Tags created
`Photoshop:PhotoshopThumbnail`  
`Photoshop:JPEG_Quality`  
`Photoshop:ResolutionInfo`  
`Photoshop:DisplayInfo`  
`Photoshop:BorderInformation`  
`Photoshop:PrintFlags`  
`Photoshop:DuotoneImageInfo`  
`Photoshop:XMLData`  
`Photoshop:RawImageMode`  
`Photoshop:Slices`  
`Photoshop:EffectsVisible`  
`Photoshop:VersionInfo`

### 3 Source
https://exiftool.org/forum/index.php?msg=6102

## pix4d.config and MicaSense.config
Tags specific for Pix4d drone mapping software and MicaSense  
Some of `XMP-Camera` tags are duplicated between the two. The `MicaSense.config` contains the `XMP-DLS` and `XMP-MicaSense` groups. It seems to be directly from the manufacturer

### MicaSense.config
#### 1 Description
More data needed  
There are fewer `XMP-Camera` tags and an incorrect duplicate of `Bandname` (lower case 'n') which should be removed. Differences in `XMP-Camera` can be see by this link  
https://www.diffchecker.com/FKawOL2U/

#### 2 Tags created
`XMP-Camera:AboveGroundAltitude`  
`XMP-Camera:BandName`  
`XMP-Camera:Bandname`  
`XMP-Camera:BandSensitivity`  
`XMP-Camera:CentralWavelength`  
`XMP-Camera:GPSXYAccuracy`  
`XMP-Camera:GPSZAccuracy`  
`XMP-Camera:Irradiance`  
`XMP-Camera:IrradiancePitch`  
`XMP-Camera:IrradianceRoll`  
`XMP-Camera:IrradianceYaw`  
`XMP-Camera:IsNormalized`  
`XMP-Camera:ModelType`  
`XMP-Camera:PerspectiveDistortion`  
`XMP-Camera:PerspectiveFocalLength`  
`XMP-Camera:PerspectiveFocalLengthUnits`  
`XMP-Camera:Pitch`   
`XMP-Camera:PrincipalPoint`  
`XMP-Camera:RigCameraIndex`  
`XMP-Camera:RigName`  
`XMP-Camera:RigRelatives`  
`XMP-Camera:Roll`  
`XMP-Camera:SensorBitDepth`  
`XMP-Camera:SerialNumber`  
`XMP-Camera:VignettingCenter`  
`XMP-Camera:VignettingPolynomial`  
`XMP-Camera:WavelengthFWHM`  
`XMP-Camera:Yaw`  
`XMP-DLS:Bandwidth`  
`XMP-DLS:CenterWavelength`  
`XMP-DLS:DirectIrradiance`  
`XMP-DLS:EstimatedDirectLightVector`  
`XMP-DLS:HorizontalIrradiance`  
`XMP-DLS:Pitch`  
`XMP-DLS:Roll`  
`XMP-DLS:ScatteredIrradiance`  
`XMP-DLS:Serial`  
`XMP-DLS:SolarAzimuth`  
`XMP-DLS:SolarElevation`  
`XMP-DLS:SpectralIrradiance`  
`XMP-DLS:SwVersion`  
`XMP-DLS:TimeStamp`  
`XMP-DLS:Yaw`  
`XMP-MicaSense:BootTimestamp`  
`XMP-MicaSense:CaptureId`  
`XMP-MicaSense:DarkRowValue`  
`XMP-MicaSense:FlightId`  
`XMP-MicaSense:ImagerTemperatureC`  
`XMP-MicaSense:PressureAlt`  
`XMP-MicaSense:RadiometricCalibration`  
`XMP-MicaSense:TriggerMethod`  

#### 3 Source
https://exiftool.org/forum/index.php?msg=56094

### pix4d.config
#### 1 Description
More data needed  
https://www.pix4d.com/
Error with the `CentralWaveLength`/`CentralWavelength` tag. One has uppercase L, the other a lowercase one.

#### 2 Tags created
`XMP-Camera:AboveGroundAltitude`  
`XMP-Camera:Albedo`  
`XMP-Camera:BandName`  
`XMP-Camera:BandName`  
`XMP-Camera:BandSensitivity`  
`XMP-Camera:BlackCurrent`  
`XMP-Camera:CalibrationPicture`  
`XMP-Camera:CaptureUUID`  
`XMP-Camera:CentralWavelength`  
`XMP-Camera:CentralWaveLength`  
`XMP-Camera:ColorTransform`  
`XMP-Camera:FisheyeAffineMatrix`  
`XMP-Camera:FisheyeAffineSymmetric`  
`XMP-Camera:FisheyePolynomial`  
`XMP-Camera:FlightUUID`  
`XMP-Camera:GPSXYAccuracy`  
`XMP-Camera:GPSZAccuracy`  
`XMP-Camera:GyroRate`  
`XMP-Camera:IMUAngularVelocity`  
`XMP-Camera:IMUFrequency`  
`XMP-Camera:IMULinearVelocity`  
`XMP-Camera:IMUPitchAccuracy`  
`XMP-Camera:IMURollAccuracy`  
`XMP-Camera:IMUSampleSize`  
`XMP-Camera:IMUTimeOffset`  
`XMP-Camera:IMUYawAccuracy`  
`XMP-Camera:InvalidPixel`  
`XMP-Camera:IrradianceRelativeRotation`  
`XMP-Camera:IsNormalized`  
`XMP-Camera:LineReadoutTime`  
`XMP-Camera:ModelType`  
`XMP-Camera:NominalCameraDistance`  
`XMP-Camera:PerspectiveDistortion`  
`XMP-Camera:PerspectiveFocalLength`  
`XMP-Camera:PerspectiveFocalLengthUnits`  
`XMP-Camera:Pitch`  
`XMP-Camera:PrincipalPoint`  
`XMP-Camera:ReflectArea`  
`XMP-Camera:RigCameraIndex`  
`XMP-Camera:RigName`  
`XMP-Camera:RigRelatives`  
`XMP-Camera:Roll`  
`XMP-Camera:SensorBitDepth`  
`XMP-Camera:SensorTemperature`  
`XMP-Camera:SunSensor`  
`XMP-Camera:SunSensorExposureTime`  
`XMP-Camera:SunSensorPitch`  
`XMP-Camera:SunSensorRelativeRotation`  
`XMP-Camera:SunSensorRoll`  
`XMP-Camera:SunSensorSensitivity`  
`XMP-Camera:SunSensorYaw`  
`XMP-Camera:TransformAlpha`  
`XMP-Camera:TransformBeta`  
`XMP-Camera:TransformGamma`  
`XMP-Camera:VignettingCenter`  
`XMP-Camera:VignettingPolynomial`  
`XMP-Camera:VignettingPolynomial2D`  
`XMP-Camera:VignettingPolynomial2DName`  
`XMP-Camera:WavelengthFWHM`  
`XMP-Camera:Yaw`  

#### 3 Source
Now included in the main archive (move this to depricated?)  
https://github.com/exiftool/exiftool/blob/master/config_files/pix4d.config

Older versions  
https://exiftool.org/forum/index.php?msg=45083  
https://exiftool.org/forum/index.php?msg=58806

## Pixel Aspect Ratio
### 1 Description
Combine fields reporting Pixel Aspect Ratio

### 2 Tags created
`Composite:PAR`

### 3 Source
https://exiftool.org/forum/index.php?msg=63600

## PNG `Palette`/`Transparency` replacements
### 1 Description
Extracts color data in human readable form from the PNG `Palette`/`Transparency` tags

### 2 Tags created
`PNG:Palette`  
`PNG:Transparency`

### 3 Source
https://exiftool.org/forum/index.php?msg=85256

## Read Windows Zone ID from Alternate Data Stream
### 1 Description
On Windows when browsers download a file, they save some data in a Windows Alternate Data Stream (ADS). This config extracts the data.

This is an example of reading other files from a config file.

### 2 Tags created
`Composite:ZoneID`  
`Composite:ZoneIDReferrerUrl`  
`Composite:ZoneIDHostUrl`  

### 3 Source
https://exiftool.org/forum/index.php?msg=76121

## RemoveRegionInfoDuplicates.config
### 1 Description
Removes MWG and Microsoft regions with duplicated names. Relies **only** on the name and does not compare the actual region size data

### 2 Tags created
`Composite:RemoveRegionInfoDuplicates`  
`Composite:RemoveRegionInfoMPDuplicates`

### 3 Source
https://exiftool.org/forum/index.php?msg=40891

## Replacement GPS tags
### 1 Description
`GPSLatitude`/`GPSLongitude` tags are fixed format, meaning you can't override the data written with the [`-n` (`--printConv`) option](https://exiftool.org/exiftool_pod.html#n---printConv). In this case, the user needed to write blank GPS entries to an XMP sidecar to prevent their main program from using the incorrect data that was embedded in the file

### 2 Tags created
`XMP-exif:GPSLatitude`  
`XMP-exif:GPSLongitude`

### 3 Source
https://exiftool.org/forum/index.php?msg=76643

## StateAbbrev.config

### 1 Description
Returns US/Canada/Mexico State Abbreviations from State/Province-State data in the file. Also contains `MyNormalize()` helper function

### 2 Tags created
`Composite:StateAbbrev`

### 3 Source
https://exiftool.org/forum/index.php?msg=44673

## TesseractOCR
### 1 Description  
This will run `tesseract` to OCR an image and return the results, which then can be copied to other tags, such as `Description`.  
### 2 Tags created  
`Composite:TesseractOCR`
### 3 Source
https://exiftool.org/forum/index.php?msg=88106

## Unicode `UserComment`
### 1 Description
Redefines `UserComment` to force encoding in unicode

### 2 Tags created
`EXIF:UserComment`

### 3 Source
https://exiftool.org/forum/index.php?topic=14078#msg75778

## VRA Core Essentials
### 1 Description
Visual Resources Association `XMP-vrae` tags

### 2 Tags created
Extensive, includes many structured tags, see Github link below

### 3 Source
Need to verify exact post in this thread  
https://exiftool.org/forum/index.php?msg=66841

### 4 Notes
https://github.com/MetadataDeluxe/VRA-Core-Essentials-ExifTool-config  
[http://metadatadeluxe.pbworks.com/w/page/20792294/VRA Embedded Metadata Subcommittee](http://metadatadeluxe.pbworks.com/w/page/20792294/VRA%20Embedded%20Metadata%20Subcommittee)

## Writing Unknown Sony tags
### 1 Description
This was an attempt by @Gerein to decode the embedded lens-profiles in Sony's ARW (v2.3.1). The `SR2_tag 0x797d` appears to now be the [`VignettingCorrParams`](https://exiftool.org/TagNames/Sony.html#SR2SubIFD)

### 2 Tags created
(part of the `Sony` makernotes group?)  
`Sony_tag`  
`SR2_tag`

### 3 Source
https://exiftool.org/forum/index.php?msg=32412

## xinet xmp tags
### 1 Description
For use with Xinet Digital Asset Management (DAM) program(?)

### 2 Tags created
`XMP-xinet:AM_ImageType`  
`XMP-xinet:AM_Status`  
`XMP-xinet:LastMetadataChange`  
`XMP-xinet:usage_locked`

### 3 Source
https://exiftool.org/forum/index.php?msg=23820  
work duplicated here  
https://exiftool.org/forum/index.php?msg=36775  

## XMP X/YPosition tags
### 1 Description
Tags to copy the `EXIF:XPosition`/`EXIF:YPosition` tags in XMP, adding them to the `XMP-tiff` namespace

### 2 Tags created
`XMP-tiff:XPosition`  
`XMP-tiff:YPosition`

### 3 Source
https://exiftool.org/forum/index.php?msg=7117
## XMP-calibre tags
### 1 Description
Tags use by the the Calibre E-book management program
### 2 Tags created 
`XMP-calibre:author_link_map`  
`XMP-calibre:author_sort`  
`XMP-calibre:custom_metadata`  
`XMP-calibre:link_maps`  
`XMP-calibre:rating`  
`XMP-calibre:series`  
`XMP-calibre:series_index`   
`XMP-calibre:timestamp`  
`XMP-calibre:title_sort`  
`XMP-calibre:user_categories`  
### 3 Source
https://exiftool.org/forum/index.php?msg=81567

# 2 Useful posts on user-defined tags
## Adding a warning response to a User Defined Tag
https://exiftool.org/forum/index.php?msg=84701

## Example of user defined tag with translations
https://exiftool.org/forum/index.php?msg=84363

## Generate a user-defined tag only if requested

https://exiftool.org/forum/index.php?msg=64529

```
ValueConv => q{
        return undef unless $$self{REQ_TAG_LOOKUP}{lower_case_tag_name};
        ...
    },
```

This way does not obey the `-api requestall` option.   
To do, Create code to make the other way work and see if that will obay the `-api` call

## How to get the tag name of a `$val[#]`
https://exiftool.org/forum/index.php?msg=83979

## How to set a user defined tag as `Time` group tag
Example from the Guano.Config

The key parts are the `PrintConv` line and the `Groups` line

```
        GuanoTimestamp => {
            Require => {
                0 => 'Description',
            },
            Groups => { 2 => 'Time' },
            PrintConv => '$self->ConvertDateTime($val)',
            ValueConv => q{
                return (($val[0]=~m/Timestamp:\s+(.*)/m)) ? $1 : undef;
            },
        },
```

## Sample Quicktime config file
https://exiftool.org/forum/index.php?msg=80852

## Storing binary data in XMP tag
You can not store arbitrary binary data in XMP.  Commonly Base64 is used to encode data like this.   
https://exiftool.org/forum/index.php?msg=82170

# 3 Deprecated/Replaced/Built in User Configs
These are user-defined config files that have been merged into the standard exiftool code, are available as stand alone config files in the [standard exiftool archive](https://github.com/exiftool/exiftool/tree/master/config_files), or have been deprecated in some other way.  They can often be used as a source on how to create user defined config files.

## age.config
### 1 Description
Figures out age between given parameter and timestamp of image. Useful for figuring out the current age of a person in the image. Moved into the main distribution.

### 2 Tags created
`Composite:Age`

### 3 Source
https://exiftool.org/forum/index.php?msg=40977

## Bibble tags
### 1 Description
XMP tags in the `XMP-dmf` group. Replaced by version on GitHub

### 2 Tags created
Structured tag with extensive (450+) subtags  
Too many to list

### 3 Source
Original Thread  
https://exiftool.org/forum/index.php?msg=38631  
Current Version  
https://github.com/exiftool/exiftool/blob/master/config_files/bibble.config

## BlueSkySea DV688
### 1 Description
config file for gps data from a BlueSkySea DV688 dashcam  
Replaced by built in version(?)

### 2 Tags created
`Composite:Accelerometer`  
`Composite:AccelerometerData`  
`Composite:GPSDateTime`  
`Composite:GPSLatitude`  
`Composite:GPSLongitude`  
`Composite:GPSSpeed`

### 3 Source
https://exiftool.org/forum/index.php?msg=54808

## Canon DustRemovalData
### 1 Description
As title, the dust removal data that can be used to fix an image. Replaced by built in version

### 2 Tags created
`Canon:DustRemovalData`

### 3 Source
https://exiftool.org/forum/index.php?msg=6091

## Check Orientation (horizontal/verticle)
### 1 Description
Returns `H` or `V` if the file is landscape or portrait

### 2 Tags created
`Composite:HorV`

### 3 Source
https://exiftool.org/forum/index.php?msg=78904

### 4 Notes
The [Aspect Ratio config](#aspect-ratio-config) includes this ability and is a better choice.

## Extract Thumbnail with proper `Orientation`
### 1 Description
Extracts thumbnail with proper rotation  
Replace by `SetTags` [Helpler Function](https://exiftool.sourceforge.net/exiftool_pod.html#Helper-functions)

### 2 Tags created
`Composite:RotatedThumbnail`

### 3 Source
https://exiftool.org/forum/index.php?msg=63389

## Formatted date composite tags
### 1 Description
A batch of tags used to format dates. Replaced by the [`-d` (`-dateFormat`) option](https://exiftool.org/exiftool_pod.html#d-FMT--dateFormat) or advanced formatting.

### 2 Tags created
`Composite:MyYear`  
`Composite:MyMonth`  
`Composite:MyDay`  

### 3 Source
https://exiftool.org/forum/index.php?msg=7536

## Fotostation Custom IPTC IIM records
### 1 Description
Fotoware Fotostation CustomFields  
Replaced and expanded by fotoware.config in main distribution

### 2 Tags created
`IPTC:CustomField01`  
through  
`IPTC:CustomField10`  

### 3 Source
Original  
https://exiftool.org/forum/index.php?topic=5336#msg25878  
Replacement  
https://github.com/exiftool/exiftool/blob/master/config_files/fotoware.config

## FullFileName
### 1 Description
Replaced with built in `FilePath` , which gives the absolute path. Returns combined `Directory` and `FileName` tags. May be a relative path

### 2 Tags created
`Composite:FullFileName`

### 3 Source
https://exiftool.org/forum/index.php?msg=29137

## gdepth.config
### 1 Description
Google Depth Map  
Now built in [XMP GDepth Tags](https://exiftool.org/TagNames/XMP.html#GDepth)

### 2 Tags created
See above link

### 3 Source
https://exiftool.org/forum/index.php?msg=44109

## GeoTiff block tags
### 1 Description
Allows copying GeoTiff data as a block  
Replaced with built in `GeoTiffDirectory`/`GeoTiffDoubleParams`/
`GeoTiffAsciiParams`

### 2 Tags created
`EXIF:GeoTiffDirectory`  
`EXIF:GeoTiffDoubleParams`  
`EXIF:GeoTiffAsciiParams`  

### 3 Source
https://exiftool.org/forum/index.php?msg=27253

## Google's Other Container tags
### 1 Description
Another set of Google Container tags which conflict with previous Google Container tags. Deprecated as this is now part of the main program

### 2 Tags created
research needed

### 3 Source
https://github.com/exiftool/exiftool/issues/254#issuecomment-2158379465

## Grab first or last four characters of tag name
### 1 Description
Creates a tag to use either the first or last four charactters of the `FileNumber` tag. Replaced by Advanced Formatting

### 2 Tags created
`Composite:MyFileNumber`

### 3 Source
https://exiftool.org/forum/index.php?msg=7189

## Photoshop Resolution tags config
### 1 Description
Allows the setting of Photoshop resolution tags  
Replaced by built in tag

### 2 Tags created
`Photoshop:ResolutionInfo`

### 3 Source
https://exiftool.org/forum/index.php?msg=16864

## ReelName.config
### 1 Description
Extracts Quicktime ReelName data  
Now built in [Quicktime:UserData](https://exiftool.org/TagNames/QuickTime.html#UserData)

### 2 Tags created
See above link

### 3 Source
https://exiftool.org/forum/index.php?msg=41954

## tiff_version.config
### 1 Description
Checks to see if TIFF is version 5 or 6

### 2 Tags created
`Composite:TIFFVersion`

### 3 Source
Original thread  
https://exiftool.org/forum/index.php?msg=53068  
Current version  
https://github.com/exiftool/exiftool/blob/master/config_files/tiff_version.config




[0x7FFC41FA68C0] ANOMALY: meaningless REX prefix used
[0x7FFC41FA6B00] ANOMALY: meaningless REX prefix used
[0x7FFC41ED9890] ANOMALY: meaningless REX prefix used
[0x7FFC41ED83F0] ANOMALY: meaningless REX prefix used
[0x7FFC41ED9B90] ANOMALY: meaningless REX prefix used
[0x7FFC41FA67A0] ANOMALY: meaningless REX prefix used
[0x7FFC43BBE380] ANOMALY: use of REX.w is meaningless (default operand size is 64)
[0x7FFC43BC0D00] ANOMALY: use of REX.w is meaningless (default operand size is 64)
