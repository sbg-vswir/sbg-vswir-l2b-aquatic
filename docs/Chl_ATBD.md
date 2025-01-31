# SBG VSWIR Aquatic Biogeochemistry - Algorithm Theoretical Basis Document (ATBD)

Kelly Luis¹, Christine Lee¹, David R. Thompson¹, Philip G. Brodrick¹, Niklas Bohn¹, Regina Eckert¹, Robert O. Green¹, K. Dana Chadwick¹, others (TBD)

*Kelly Luis**<sup>1</sup>

<sup>1</sup>Jet Propulsion Laboratory, California Institute of Technology

Corresponding author: Kelly Luis (kelly.m.luis@jpl.nasa.gov)

**Key Points:**

**Version:** 1.0

**Release Date:** TBD

**DOI:** TBD

## Abstract
This ATBD retrieves chlorophyll concentration and spectral inherent optical properties (IOPs) using a modular structure for deriving aquatic biogeochemistry products in inland, nearshore, open ocean waters. The derived products include chlorophyll a concentration and phytoplankton absorption coefficient, aph(λ) [units: m-1]. For inland and nearshore waters, the Aquaverse environment (Pahlevan et al. 2021, etc.) and the Generalized Inherent Optical Property-Default Configuration (GIOP-DC) is used for open ocean waters (Werdell et al. 2013).  

## Plain Language Summary

Water quality is a measure of suitability of water based on its physical, biological, and chemical characteristics. This algorithm workflow enables biological and physical descriptions of water via continuous observations between the visible to near-infrared portion of the electromagnetic spectrum. Chlorophyll a concentration is a measure of a pigment found in phytoplankton, and inherent optical properties describe the absorption and scattering of particles in water. This workflow focuses on the phytoplankton absorption coefficient, the absorption characteristics of phytoplankton. The chlorophyll a concentration provides an understanding of photosynthesis by the overall phytoplankton community composition (PCC). while the phytoplankton absorption coefficient provides a steppingstone to delineating phytoplankton groups contributing the PCC. 


### Keywords: chlorohyll,inherent optical properties, water quality

## 1 Version Description

This is Version 1.0 of the SBG-VSWIR Aquatic Biogeochemistry algorithm. It builds on the lineage of ocean color algorithms from the Ocean Biology Processing Group (OBPG). 
## Plain Language Summary

### Keywords: 

## 1 Version Description

This is Version 1.0 of the SBG VSWIR a

## 2 Introduction

Following on recommendations by the National Academies of Science, Engineering and Medicine in their 2017 Decadal Survey on Earth Sciences, the National Aeronautics and Space Administration (NASA) selected the Surface Biology and Geology (SBG) mission for implementation as part of its Earth System Observatory (ESO).  SBG in particular aims to measure properties of the Earth’s surface composition and ecology.  It is comprised of two platforms: a wide-swath thermal infrared instrument on a free-flying spacecraft in a polar orbit with an afternoon equatorial crossing time; and a separate spacecraft carrying a wide-swath solar reflectance imaging spectrometer operating in the Visible Shortwave Infrared (VSWIR), with a morning equatorial crossing time.  SBG-VSWIR will measure the solar reflected range at approximately 380-2500 nm at 10 nm spectral sampling, over a 180 km swath with 30 m spatial sampling.  This measurement enables repeat coverage of any location on Earth every 16 days.  The visible-shortwave infrared range is sensitive to diverse physical processes in the Earth’s surface and atmosphere (Cawse-Nicholson 2021). The spectral, spatial, and radiometric resolutions of the SBG VSWIR instrument will enable Earth-system-scale measurements of aquatic ecosystems, including biogeochemistry products across inland, nearshore coastal, and open ocean ecosystems.  

Thus, this algorithm theoretical basis document describes the algorithm process used to derive chlorophyll and inherent optical properties within the L2+ Aquatic Biogeochemistry and Composition section of the SBG-VSWIR aquatic workflow (Figure 1). 


## 3 Context/Background

### 3.1 Historical Perspective
From 1978-1986, the Coastal Zone Color Scanner (CZCS) was the first satellite instrument dedicated to observing ocean color, the visible wavelengths of the upper sunlit ocean. A key product was the near surface chlorophyll a, dominant pigment responsible for photosynthesis in phytoplankton. Subsequent missions such as SeaWiFS, MODIS, MERIS, VIIRS, OLCI, and PACE have built on the success of CZCS to provide bio-optical estimations such as inherent optical properties (IOPs), absorption and scattering properties that do not change with the ambient light field. These foundational bio-optical estimations provide a steppingstone to developing algorithms for characterizing phytoplankton community composition and other water column constituents important for the stud of water quality.  

### 3.2 Additional Information
With the launch of PACE, NASA’s first hyperspectral satellite dedicated ocean color observations, in February 2024, advancements in imaging spectroscopy or hyperspectral algorithms are expected to abound in the upcoming years. For that reason, this ATBD version relies on heritage and open-source algorithms that have been based on a combination of multispectral and spectroscopic and hyperspectral algorithms. 

### 3.2 Additional Information

## 4 Algorithm Description

### 4.1 Scientific Theory

#### 4.1.2 Scientific theory assumptions

### 4.2 Mathematical Theory

#### 4.2.1 Mathematical theory assumptions

### 4.3 Algorithm Input Variables

| Name | Long name                     | Unit  |
|------|--------------------------------|-------|
| Rrs  | Remote Sensing Reflectance    | sr⁻¹  |

### 4.4 Algorithm Output Variables

| Name    | Long name                                  | Unit   |
|---------|-------------------------------------------|--------|
| chlor_a | Chlorophyll a                             | mg m⁻³ |
| aph     | Phytoplankton absorption coefficient     | 1/m    |

=======
### 4.4 Algorithm Output Variables

## 5 Algorithm Usage Constraints

## 6 Performance Assessment

### 6.1 Validation Methods

### 6.2 Uncertainties

### 6.3 Validation Errors

## 7 Algorithm Implementation

### 7.1 Algorithm Availability

### 7.2 Input Data Access

### 7.3 Output Data Access

### 7.4 Important Related URLs

## 8 Significance Discussion

## 9 Open Research

## 10 Acknowledgements

## 11 Contact Details

## References