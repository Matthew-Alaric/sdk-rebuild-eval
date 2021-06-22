# Glasswall Rebuild Evaluation SDK - Changelog
All notable changes to this project will be documented in this file. It is only updated periodically to align with 
published releases or significant updates to this repository.

## Known Issues
-	In Export Mode, The UTF-8 encoding has not been applied to all extracted text, which means that some exported text is not UTF-8 compliant.
-       Some minor regression issues for DOC files in this build becasue of Lite camera changes


# 2021-06-21

### Rebuild v1.1850
#### General Remarks

This is a pre release with extended support for GeoTiff files. The build contains extended validation and content 
management policy options for GeoTiff files. This is not an official release.

This build has been branched off from Rebuild version 1.185.

#### Breaking changes

- Updates to content management policy settings schema to include additional GeoTiff policy options. 

#### Key Known Issues

- Depending on policy settings, geo key entries are removed but some of its corresponding data may still be present in 
the regenerated document.
- The ability to update offsets upon removal of tags has not yet been implemented, the data is cleared and therefore 
redundant but this results in a file that may contain snippets of redundant data.
- Some big endian GeoTiff files are incorrectly marked non conforming.
- Analysis report does not contain a full summary of the Geo Tiff policy settings applied.