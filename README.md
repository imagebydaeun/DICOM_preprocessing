# 💻 DICOM Preprocessing & Registration

![Python](https://img.shields.io/badge/Python-3.10-blue.svg)
![AntsPy](https://img.shields.io/badge/AntsPy-0.5.4-green)
![SimpleITK](https://img.shields.io/badge/SimpleITK-2.4.1-yellow)

<br>
This repository provides a preprocessing pipeline for liver T1 dynamic MRI datasets consisting of pre / AP / PP phases.

<br>
<br>

<details>
<summary>📁 <strong>Input Data Types & Folder Structure (Click to expand)</strong></summary>

<br/>

- Input structures can be in 2 types:


#### 1. Converted NRRD files
```
BASE_DIR/
└── patient_id/
    ├── pre.nrrd
    ├── AP.nrrd
    └── PP.nrrd
```

#### 2. Raw DICOM directories
```
BASE_DIR
└── patient_id
    ├── pre
    │   └── *.dcm
    ├── AP
    │   └── *.dcm
    └── PP
        └── *.dcm
```
</details>

<details>
<summary>📁 <strong>Output Data Types & Folder Structure (Click to expand)</strong></summary>
<br/>

- Registration was done as **PP as fixed image**


```
BASE_DIR
└── patient_id
    ├── pre_reg.nii.gz
    ├── AP_reg.nii.gz
    └── PP.nii.gz
```
</details>
<br>
<br>

## 🎯 Purpose
To **match the geometric metadata** (e.g., voxel spacing, direction, origin) of multi-phase liver MRI images **prior to registration**, ensuring accuracy and alignment consistency.
<br>
<br>
<br>
<br>


## ⚙️ Workflow Pipeline
<br/>

### 1️⃣ Check Geometry Matching
- 📄 `check_matching_before_registration.ipynb`
- ✅ Identifies geometry mismatch across pre / AP / PP images

<br/>

### 2️⃣ Match Geometry Before Registration
There are 2 types of matching methods:


**1. Resampling**
- 📄 `resampling_to_match_before_registration.ipynb`
- 🔧 Uses **linear interpolation** to match geometry

**2. FOV Cropping (requires raw DICOMs)**
- 📄 `cropFOV_to_match_before_registration.ipynb`
- ✂️ Matches z-range without interpolation

<br/>

### 3️⃣ Apply Registration
- 🔁 Perform **Rigid**, **Affine**, or **SyN** registration with ANTsPy
- 📄 `SYNregistration.ipynb`
- Set `transform_type=` in your script:
    `'rigid'`
    `'affine'`
    `'SyN'`

<br>
