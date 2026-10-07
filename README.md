# MMFogEcho
Official repository for the MMFogEcho real-fog multimodal dataset.

**MMFogEcho** is a real-fog multimodal dataset associated with our work on LiDAR echo-based measurement under foggy conditions.

## Overview

The dataset was collected under controlled real-fog conditions for the study of multimodal LiDAR echo processing and measurement in scattering environments. The experimental platform incorporates LiDAR and imaging sensors to capture complementary information under different conditions.

## Files

| Path | Contents |
| --- | --- |
| README.md | Dataset introduction, file structure and annotation descriptions |
| Scenes/scene_XX/echoes/N/*.bin | Raw LiDAR waveforms |
| Scenes/scene_XX/images/N.png | RGB images temporally paired with echoes using acquisition timestamps |
| Scenes/scene_XX/annotations.json | Labels for echo–image pairs, including target, reference distance, scanning angles and optical thickness |
| Calibration/camera_lidar.json | Calibration parameters: camera intrinsic parameters, LiDAR-to-camera extrinsic parameters, and coordinate conventions |
| Metadata/data_format.json | Echo and image format specifications |
| Metadata/data_usage.md | Data usage instructions for point cloud reconstruction and echo-to-image associations |

## Annotations

Annotations are stored as a JSON array in each scene. Echo and image paths are relative to the containing scene directory.

| Field | Meaning |
| --- | --- |
| echo | Relative path to the waveform file |
| image | Relative path to the temporally paired RGB image |
| reference_depth_m | Reference target distance in metres |
| angle.azimuth_deg | Azimuth angle in degrees |
| angle.elevation_deg | Elevation angle in degrees |
| target | Target label; `refXX` denotes a Lambertian panel with XX% reflectance |
| OT | Optical thickness |

## Citation

If you use the dataset resources released through this repository in your research, please cite the associated paper.

Citation information will be updated upon publication.