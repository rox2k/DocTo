# DocTo

Simple utility for converting a Microsoft Word Document '.doc' file to any other supported format 
such as .txt .rtf .pdf.  

Can also be used to convert .txt, .rtf to .doc or .pdf format.

Must have Microsoft Word installed on host machine.

Download Release From Github Releases - https://github.com/tobya/DocTo/releases/
Further Information available at http://tobya.github.com/DocTo

## Features

  1. Convert Doc/RTF/Text file to any Word SaveAs Type Doc/Text/RTF/PDF
  1. Single File Conversion
  1. Multiple / Directory File Conversion
  1. Delete after conversion
  1. Fire Webhook one each conversion.
  

## Updates

0.7     Added support for saveas2 function added by microsoft in Word 2010.  Additional Switches.

0.5.5   Changes made to logging.  -Q and -L 0 now work correctly ensuring nothing is output to console.  Must specify -G or -GL to get access to logs and errors.
                                Also -L 10 now outputs extra as logging param is loaded first.


## Examples

### Single

Convert Microsoft Word Document to text

    docto -f C:\Directory\MyFile.doc -O "C:\Output Directory\MyTextFile.txt" -T wdFormatText

Convert Microsoft Word Document to PDF (requires version of Microsoft Word that supports this).

     docto -f C:\Directory\MyFile.doc -O "C:\Output Directory\MyTextFile.pdf" -T wdFormatPDF

### Multiple Files and Folders

Convert All Microsoft Word Documents in Directory and its Sub Directories to PDF

    docto -f "C:\Dir with Spaces\FilesToConvert\" -O "C:\DirToOutput" -T wdFormatPDF  -OX .pdf

Delete Origional Files after conversion.

    docto -f "C:\Dir with Spaces\FilesToConvert\" -O "C:\DirToOutput" -T wdFormatPDF  -OX .pdf -R

Webhooks
========

Add a Webhook to fire on each conversion

    docto -f "C:\Dir with Spaces\FilesToConvert\" -O "C:\DirToOutput" -T wdFormatPDF  -OX .pdf  -R -W http://toflidium.com/webhooks/docto/webhook_test.php


## Command Line Help

     docto -h


    Help
    Version:0.6.6
    Source: http://github.com/tobya/DocTo/
    Command Line Parameters
    Each Parameter should be followed by its value  -f "c:\Docs\MyDoc.doc" -O "C:\MyDir\MyFile"
      -H  This message
      -F  Input File or Directory
      -FX Input Extension to search for if directory.  Default ".doc" (will find ".docx" also)
      -O  Output File or Directory to place converted Docs
      -OX Output Extension if -F is Directory.
      -T  Format(Type) to convert file to, either integer or wdSaveFormat constant.
          Available from http://msdn.microsoft.com/en-us/library/microsoft.office.interop.word.wdsaveformat.aspx  or
          http://msdn.microsoft.com/en-us/library/office/bb241279(v=office.12).aspx
          See current List Below.
      -TF Force Format.  -T value if integer is checked against current list compiled in and not passed if unavailable.
          To future proof, -TF will pass through value without checking.
          Word will return an "EOleException  Value out of range" error if invalid.
          Use instead of -T.
      -L  Log Level 1 Errors Only, 2 Standard, 5 CHATTY, 10 VERBOSE
          Default: 2 Standard
      -C  Compatibility Mode. Set to an INTEGER value from https://msdn.microsoft.com/en-us/library/office/ff192388.aspx.
      -M  Ignore all files in __MACOSX\ subdirectory if it exists.  Default True.
      -G  Write Log to file in directory
      -GL Log File Name to Use default 'DocTo.Log';
      -Q  Quiet Mode: Nothing will be output to console.  To see any errors you must set -G or -GL
          Equivalent to setting -L 0
      -R  Remove Files after successful conversion: Default false;
      -W  Webhook: Url to call on events (plain url no params). See -HW for more details.
      -HW Webhook Help.
      -X  Halt on COM Error: Default True;  If you have trouble with some files not converting, set this to false to ignore
          errors and continue with batch job.
      -V  Show Versions.  DocTo and Word/Excel


    ERROR CODES:
    200 : Invalid File Format specified
    201 : Insufficient Inputs.  Minimum of Input File, Output File & Type
    202 : Incorrect switches.  Switch requires value
    203 : Unknown switch in command
    220 : Word or COM Error
    221 : Word not Installed

    COMPATIBILITY MODES:
    FROM https://msdn.microsoft.com/en-us/library/office/ff836084.aspx

    wdCurrent   : 65535 (Compatibility mode equivalent to the latest version of Microsoft Word.)
    wdWord2003  : 11  Word 2010 is put into a mode that is most compatible with Word 2003. Features new to Word 2010 are
                      disabled in this mode.
    wdWord2007  : 12  Word 2010 is put into a mode that is most compatible with Office Word 2007. Features new to Word 2010
                      are disabled in this mode.
    wdWord2010  : 14  Word 2013 is put into a mode that is most compatible with . Features new to Word 2013
                      are disabled in this mode.
    wdWord2013  : 15  Default. All Word 2013 features are enabled.

Options
=======

