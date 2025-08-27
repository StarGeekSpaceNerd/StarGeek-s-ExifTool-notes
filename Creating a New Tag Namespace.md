# Creating a new tag namespace
Important note: Do **not** use a word processor/Google Docs or similar programs to create a config file. Those programs will "help" you by changing certain characters to the correct ones needed for printed text, but are unacceptable for code.

1. Extract the raw XMP data with this command. Either save it to a file or copy/paste it into a text editor.
`exiftool -b -xmp file.jpg`
2. Use the command in [FAQ #3](https://exiftool.org/faq.html#Q3) to list the data you want to add. Look at the group the new tags belong to. This will be enclosed by brackets and start with `XMP-`.  For example, `[XMP-dc]`. The text after the dash is the group name. In this example, the group name is `dc`.
3. Create a file and copy/paste this code into it. This is the core code copied from the [`example.config` file](https://exiftool.org/config.html).
```
# The %Image::ExifTool::UserDefined hash defines new tags to be added
# to existing tables.
%Image::ExifTool::UserDefined = (
    # new XMP namespaces (eg. xxx) must be added to the Main XMP table:
    'Image::ExifTool::XMP::Main' => {
        # namespace definition for examples 8 to 11
        xxx => { # <-- must be the same as the NAMESPACE prefix
            SubDirectory => {
                TagTable => 'Image::ExifTool::UserDefined::xxx',
                # (see the definition of this table below)
            },
        },
	},
),

# This is a basic example of the definition for a new XMP namespace.
# This table is referenced through a SubDirectory tag definition
# in the %Image::ExifTool::UserDefined definition above.
# The namespace prefix for these tags is 'xxx', which corresponds to
# an ExifTool family 1 group name of 'XMP-xxx'.
%Image::ExifTool::UserDefined::xxx = (
    GROUPS => { 0 => 'XMP', 1 => 'XMP-xxx', 2 => 'Image' },
    NAMESPACE => { 'xxx' => 'http://ns.myname.com/xxx/1.0/' },
    WRITABLE => 'string', # (default to string-type tags)
    # Example 8.  XMP-xxx:NewXMPxxxTag1 (an alternate-language tag)
    # - replace "NewXMPxxxTag1" with your own tag name (eg. "MyTag")
    NewXMPxxxTag1 => { Writable => 'lang-alt' },
    # Example 9.  XMP-xxx:NewXMPxxxTag2 (a string tag in the Author category)
    NewXMPxxxTag2 => { Groups => { 2 => 'Author' } },
    # Example 10.  XMP-xxx:NewXMPxxxTag3 (an unordered List-type tag)
    NewXMPxxxTag3 => { List => 'Bag' },
    # Example 11.  XMP-xxx:NewXMPxxxStruct (a structured tag)
    # - example structured XMP tag
    NewXMPxxxStruct => {
        # the "Struct" entry defines the structure fields
        Struct => {
            # optional namespace prefix and URI for structure fields
            # (required only if different than NAMESPACE above)
            # --> multiple entries may exist in this namespace lookup,
            # with the last one alphabetically being the default for
            # the fields, but each field may have a "Namespace"
            # element to specify which prefix to use
            NAMESPACE => { 'test' => 'http://x.y.z/test/' },
            # optional structure name (used for warning messages only)
            STRUCT_NAME => 'MyStruct',
            # optional rdf:type property for the structure
            TYPE => 'http://x.y.z/test/xystruct',
            # structure field definitions (very similar to tag definitions)
            X => { Writable => 'integer' },
            Y => { Writable => 'integer' },
            # a nested structure...
            Things => {
                List => 'Bag',
                Struct => {
                    NAMESPACE => { thing => 'http://x.y.z/thing/' },
                    What  => { },
                    Where => { },
                },
            },
        },
        List => 'Seq', # structures may also be elements of a list
    },
    # Each field in the structure has a corresponding flattened tag that is
    # generated automatically with an ID made from a concatenation of the
    # original structure tag ID and the field name (after capitalizing the
    # first letter of the field name if necessary).  The Name and/or
    # Description of these flattened tags may be changed if desired, but all
    # other tag properties are taken from the structure field definition.
    # The "Flat" flag must be used when setting the Name or Description of a
    # flattened tag.  For example:
    NewXMPxxxStructX => { Name => 'SomeOtherName', Flat => 1 },
);
```perl

```
4. In the base code, replace the `xxx` with the group name in the following lines:  
    - Line 7: `xxx => { # <-- must be the same as the NAMESPACE prefix`  
    - Line 9: `TagTable => 'Image::ExifTool::UserDefined::xxx',`  
    - Line 21: `%Image::ExifTool::UserDefined::xxx = (`  
    - Line 22: `GROUPS => { 0 => 'XMP', 1 => 'XMP-xxx', 2 => 'Image' },`  
    - Line 23, only replace the first `xxx`. The second one will be replaced in the next step ` NAMESPACE => { 'xxx' => `  
5. Somewhere in the raw XMP, usually near the top, there is a line that starts with `xmlns:` followed by the group name, then a URI. Copy that and in line 23, replace `http://ns.myname.com/xxx/1.0/` with that value.


# Other notes
## Detecting a structured tag  
A structured tag will include `rdf:parseType='Resource'` in the tag name of the structure. For example, the XMP   
`<tps:template rdf:parseType='Resource'>`
indicates that the structured tag name is `template`. Any tags that are part of this structure will be before the closing XML, which in this case would be   
`</tps:template>`
In the exiftool output, all flattened tags for this structure with have the structure name as a prefix. For this structure, the sub-tag is `Txml`, which leads to a flattened tag name of `TemplateTxml`.