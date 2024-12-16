work in progress, ignore this for now

Run this command
`exiftool -ver -v`
Look for the line that list the verion of Perl that exiftool is using.
Example: this output shows the perl version is 5.032001, which translates to version 5.32.1
`C:\> exiftool -ver -v
ExifTool version 12.97
Perl version 5.032001 (-C0)
Platform: MSWin32
Optional libraries:
  Archive::Zip                 1.68
  Compress::Zlib               2.1`

  Look for the correct version on the [Strawberry Perl release page](https://strawberryperl.com/releases.html).  Download and install that.

  You may need to check for other versions of Perl on your system.

  Run this to check the perl version
```
C:\>perl --version

This is perl 5, version 32, subversion 1 (v5.32.1) built for MSWin32-x64-multi-thread
<snip>
```

Run
`cpanm -L C:\path\to\exiftool_files Module::ToInstall`
Example
`cpanm -L C:\Programs\UnixUtils\ExifTool\exiftool_files DateTime::TimeZone`

This creates this directory `exiftool_files\lib\perl5`. Open up the `perl5` directory and copy/paste all the files into the parent directory `\lib`. Some may be duplicates and you want to skip those, i.e. don't replace them.

The CPAN module should now work.
