# Staging module for Akoya - CODEX to MCMICRO

The codex2mc.py script stages CODEX data sets for being registered with ASHLAR in MCMICRO.

The script takes as main input the path to the cycle folder that cointains the raw tiles generated by the Akoya CODEX platform.  codex2mc.py reads these tiles and distributes them into acquisition groups. i.e tiles with common rack, well, ROI and exposure levels will be written into an ome.tiff file with the necessary metadata for registration.  To be more precise two such ome.tiff files will be generated per cycle, one corresponds to the background signal and the other to the markers signal.

## CLI
### Required arguments
| Argument|Long name|Type|Description|Default value|
|---------|---------|----|-----------|-------------|
| -i | string/path | --input | Absolute path to the the parent folder of the raw tiles, i.e. the cycle folder whose name follows the pattern X_Cycle_N,where N represents the cycle number | NA |
| -o | string/path | --output | Absolute path to the directory in which the outputs will be saved. If the output directory doesn't exist it will be created. | NA |

### Optional arguments
| Argument|Type|Long name| Description | Default value |
|---------|----|---------|-------------|---------------|
|-rm|string | --reference_marker | Name of the reference marker for registration|'DAPI'|
|-od|string | --output_dir | String specifying the name of the subfolder in which the staged images will be saved.|'raw'|
|-ic|boolean flag | --illumination_correction |Give this flag to apply illumination correction to all tiles, the illumination profiles are calculated with basicpy | FALSE |
|-he|boolean flag | --hi_exposure_only |Give this flag to extract only the set of images with the highest exposure time|FALSE|

## Container usage
### download container:
- Docker
```
docker pull ghcr.io/schapirolabor/multiplex_codex:v1.1.0
```
- Singularity
```
singularity pull docker://ghcr.io/schapirolabor/multiplex_codex:v1.1.0
```
### Script execution

- Singularity
``` bash
singularity exec --bind $path_to_your_local_cycle_folder:/mnt,$path_to_your_local_output_folder:/media --no-home $path_to_container python staging/codex2mc/codex2mc.py -i /mnt/$path_to_your_local_cycle_folder -o /media/$path_to_your_local_output_folder
```
