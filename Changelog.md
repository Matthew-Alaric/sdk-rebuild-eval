# Glasswall Rebuild Evaluation SDK - Changelog
All notable changes to this project will be documented in this file. It is only updated persiodically to align with publshed releases or significant updates to this repository.

## Known Issues
-	In Export Mode, The UTF-8 encoding has not been applied to all extracted text, which means that some exported text is not UTF-8 compliant.
-       Some minor regression issues for DOC files in this build becasue of Lite camera changes

# 2021-06-08

### Rebuild v1.241

#### Lite Modes

The Lite mode cameras have been disabled for increased stability

#### Accumulated bug fixes since last production release (1.157)

- DDE - Fix for rendering issue caused by DDE removal 
- Fix Fuzzed Doc files causing engine to hang (113996). 
- PDF: Handle empty article thread arrays correctly 
- PPTX: Fix for end of stream errors 
- TIFF: Alignment of handling with Editor (size in analysis reports, geotag validation) 
- XLSM: Fix for end of stream errors 
- PDF: Prevent early bailout when invalid image stream is encountered during syntax checking 
- XLS: file with hyperlinks needs repairing 
- XLS: Analysis report stops reporting after embedded image Issue item is reported 
- XLSM: Fix applied for repair message appearing for Threaded Comments 
- DOCX: Fix hyperlink sanitisation repair message popup 
- Fix issue with validation of MachO Segment Command length fields 
- PDF: Respect governing content management switch when reporting non-conformances in source dictionaries 
- XLSX: Linux: force free memory on the heap to be released back to the operating system 
- Non-conforming elf file causes engine to hang
- Reverted changes that incorrectly removed content that was not DDE.
- Fix for rendering issue caused by DDE removal
- Extra restrictions when gathering field codes for DDE
- Fix for crashing PDF caused by an out bounds access
- Fix for crashing PDF. Error reporting function was called with two format arguments
- Updated MP4 camera with lots of structural fixes and inclusion of missing h265 structures

# 2021-04-21

### Rebuild v1.197

#### Lite Modes

This release now includes the Lite modes for all office cameras (binary and ooxml). these are currently being QA'd but are expected to in the next full production release.

# 2021-03-31

### Rebuild v1.171

#### PDF Change

This release contains a pre-release version of digital signature sanitisation for pdf. The policy setting <digital_signatures></digital_signatures> can be set to allow to pass the signature through unchanged, sanitsiee to remove the signature and disallow to prevent the file from being regenerated. The default behaviour is sanitise so if you wish to keep the previous behaviour of not regenerating the file then a setting of disallow is required. 

# 2021-02-18

### Rebuild v1.157

#### General Remarks

This release contains a number of bug fixes across several supported file types. It has one planned improvement for geotiff processing and several Public Preview functions 

#### Bug Fixes

- Stability fixes - a number of fixes for crashes identified during penetration testing.
- Bug 114107 - Empty stream causing crash in DOC
- Bug 107044 - Prevent malicious GIF causing segmentation fault
- Bug 114068 - OLE link not sanitised in OOXML
- Bug 114508 - Fixed memory leak when importing a file that is not an archive
- Bug 114675 - Correct where big endian TIFF files were being written out as little endian and corrupting the file.

#### Other Improvements

- Content management for Geotiff files. Geotiff metadata can now be removed from geotiff files. The dafult for this switch is sanitise so users should add the following to their policy files is they wish to keep geotiff metadata:
```
    <tiffConfig>
      <geotiff>allow</geotiff>
    </tiffConfig>
```
- Header file clean up. 

#### Public Preview Functions

This release contains early versions of functionality that is being developed to improve the flexibility of the Rebuild SDK. Whilst we continue to work on these features we would gladly appreciate any feedback on what is currently available.

- Lite mode for xls and pdf. This mode implements a content management policy only regeneration mode for xls and similar for pdf although some remediations are still done. Notes on how to use this API can be found at https://docs.glasswallsolutions.com/sdk/rebuild/Content/API/Glasswall%20Document%20Processing%20-%20File%20to%20Memory%20Location.htm#GWFilePr3
- Digital signatures content management switch for pdf.  Within the pdf content management section the new switch <digital_signatures> is now avialable. Permitted settings are "allow" and "disallow". The default is disallow to match previous behaviour. If allow is set then the digital signatures are output to the regenerated file but will now be invalid because of changes to the file caused by Rebuild.

## 2020-12-01

### Rebuild v1.127

#### General Remarks

This release contains one bug fix for displaying tiff within ooxml that also resolves segmentation faults experienced by linux users. 

#### Bug Fixes

- Bug 110508 - Fix TIF Image not displaying after protect modes. Also resolves segmentation faults for some TIFF images within Office Open xml.


## 2020-11-30

### Rebuild v1.125

#### General Remarks

This release contains one bug fix for the jpeg file type. 

#### Bug Fixes

- Bug 113059 - Added additional validation on JPEG MCU dimensions to stop some crashes


## 2020-11-23

### Rebuild v1.124

#### General Remarks

This release contains a number of bug fixes across several supported file types. The default content management settings if a configuration file is not provided has been changed to sanitise.

#### Bug Fixes

- Bug 113062 - End of stream error (When parsing of Alternate Content tags)
- Bug 108386 - DDE not fully cleared in DOCX files
- Bug 113493 - Incorrect report of 'Neither 1Table or 0Table present' (Due to word binary picture document)
- Bug 113060 - PNG Segnmentation fault

#### Other Improvements

- Update to handle embedded gif files in office documents (Issue with documents generated by Office365).
- Additional uupport for H265 encoded MP4 files
- Major updates to support validation against latest MS-Office specifications. Versions: DOCX Revision 14.0, PPTX Revision 16.0, XLSX Revision 20.0 
(https://docs.microsoft.com/en-us/openspecs/office_standards/ms-offstandlp/d5784a8b-7070-466b-befa-b7bf3724c6f0)
- Improved support for TIFF images embedded within OOXML documents.


## 2020-08-11

### Rebuild v1.99

#### General Remarks

This release contains a number of bug fixes across several supported file types.
	
The Glasswall SDK Documentation is moving online. You can find it at https://docs.glasswallsolutions.com/sdk/rebuild/Content/Home.htm. 
This is a work in progress and feedback is welcome. The online documentation will become the master set so you may spot some discrepancies 
between documents during the transition period.

#### New Features

- Support for Alpine Linux - The Linux versions of the library now runs on Alpine Linux. The main change to support this was to use a new utf-8 library. If customers do experience encoding issues because of this change please repot via support.

#### Other Improvements

- Update to MS-Office Extensions version support to include recent additions. Now support extensions up to those shown in the below table: 

|     Doc Type    |     Date         |     Protocol Revision    |     Revision Class    |     Downloads      |
|-----------------|------------------|--------------------------|-----------------------|--------------------|
|     MS-PPTX     |     26/2/2020    |     16.0                 |     Major             |     PDF \| DOCX    |
|     MS-XLSX     |     19/2/2020    |     19.0                 |     Major             |     PDF \| DOCX    |
|     MS-DOCX     |     19/2/2020    |     13.0                 |     Major             |     PDF \| DOCX    |

    Features impacted by these spec updates include:

    - PPTX: 
        - Latest versions of Author and Comments. 
        - Media (tracks and track information) support on slides. 
        - Slide transitions such as preset transitions and transition effects.
    - DOCX:
        - Latest versions of comments (review comments). 
    - XLSX: 
        - Workbook calculation engine feature updates. 
        - Excel collections of key value pairs identification and fallback.
        - Filter criterion associated with key value pairs. 
        - Two-dimension arrays. 

-	Update to Office 365 support - Update to processing of Open Office xml documents (PPTX, XLSX, DOCX, etc) to deal with change in internal structures within Office 365. **Note: These changes have been made from observed changes within the file structures and do not match current published specifications. Failures observed by both Glasswall and our customers persuaded us of the need to make this change without a published specification update.**

#### Bug Fixes

|     ID        |     Description                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------|
|     105844    |     PDF's fail import with "FilterFailed" error (Ref:57832/3490)                                |
|     106564    |     Update all rootlevels structure rules                                                       |
|     106607    |     Extend the CT_Settings structure to accomodate CT_Extension                                 |
|     106804    |     DOCX  fixed repair message  after regenerating.                                             |
|     106820    |     PPT: Inconsistent results across windows/Linux analysis/protect                             |
|     106821    |     Subset of XLS files not recognised                                                          |
|     106825    |     OOXML - files with Comments, Numbered Styles need to be repaired after being regeneration   |
|     106872    |     Subset of PPTX files are not being regenerated                                              |

## 2020-07-01

### Rebuild v1.82

#### Bug Fixes
- 105844 - PDF fials import with "FilterFailed" error
- 4685 - Fix for PPT utf-16 export failure

#### Documentation
No Change.

#### Other Improvements
- Updates to PPTX support based on Microsoft specification changes.
- Support for Alipine Linux OS
