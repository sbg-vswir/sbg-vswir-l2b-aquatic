# SBG VSWIR Benthic Fractional Cover - Algorithm Theoretical Basis Document (ATBD)**

Kelly Luis¹, Christine Lee¹, David R. Thompson¹, Philip G. Brodrick¹, Niklas Bohn¹, Regina Eckert¹, Robert O. Green¹, K. Dana Chadwick¹, others (TBD)

<sup>1</sup>Jet Propulsion Laboratory, California Institute of Technology

Corresponding author: Kelly Luis (kelly.m.luis@jpl.nasa.gov)

**Key Points:**
- Benthic fractional cover types include coral, algae, sand, and seagrass.  
- Intermediary products developed include bathymetry, inherent optical properties, and benthic reflectance.  

**Version:** 1.0

**Release Date:** TBD

**DOI:** TBD

## Abstract

The SBG VSWIR benthic fractional cover algorithm retrieves coral, sand, algae, and seagrass fractional cover from shallow benthic ecosystems. Bayesian optimization retrieves the bathymetry, benthic reflectance, and inherent optical properties from remote sensing reflectance. For a pixel where bathymetry is less than five meters, a spectral unmixing algorithm references a benthic spectral library to derive benthic fractional cover estimates for coral, sand, algae, and seagrass. 

## Plain Language Summary

Shallow benthic ecosystems are biodiversity hotspots and providing an array of critical ecosystems services. Understanding large-scale shifts in the composition of these habitats is critical for preserving and protecting these ecosystems and their numerous ecosystem services and benefits. Through modeling water column scattering and absorption processes in the visible light range, bottom substrate type can be identified in shallow water aquatic ecosystems and ancillary information such as bathymetry and water quality information can be retrieved along the way
### Keywords: imaging spectroscopy, hyperspectral imaging, coral reefs 

## 1 Version Description

This is Version 1.0 of the SBG VSWIR terrestrial vegetation algorithm equivalent water thickness, sometimes referred to as canopy water content. 

## 2 Introduction
Following on recommendations by the National Academies of Science, Engineering and Medicine in their 2017 Decadal Survey on Earth Sciences, the National Aeronautics and Space Administration (NASA) selected the Surface Biology and Geology (SBG) mission for implementation as part of its Earth System Observatory (ESO).  SBG in particular aims to measure properties of the Earth’s surface composition and ecology.  It is comprised of two platforms: a wide-swath thermal infrared instrument on a free-flying spacecraft in a polar orbit with an afternoon equatorial crossing time; and a separate spacecraft carrying a wide-swath solar reflectance imaging spectrometer operating in the Visible Shortwave Infrared (VSWIR), with a morning equatorial crossing time.  SBG-VSWIR will measure the solar reflected range at approximately 380-2500 nm at 10 nm spectral sampling, over a 180 km swath with 30 m spatial sampling.  This measurement enables repeat coverage of any location on Earth every 16 days.  The visible-shortwave infrared range is sensitive to diverse physical processes in the Earth’s surface and atmosphere (Cawse-Nicholson 2021). The spectral, spatial, and radiometric resolutions of the SBG VSWIR instrument will enable Earth-system-scale measurements of aquatic ecosystems, including benthic habitat composition.  

Benthic ecosystems, including coral reefs, seagrass, kelp beds, and other submerged aquatic ecosystems, are of the most diverse and economically valuable aquatic ecosystems on the planet. In particular, coral reefs provide critical habitat for about 25% of all marine species, buffer coastlines from storm activity in more than 100 countries, and reefs sustain tourism for at least 94 countries and territories and of the 94, in a quarter of them reefs contribute 15% of the gross domestic product. However, 75% of reefs are estimated to be threatened by local stressors (e.g., coastal development and watershed-based pollution) and global stressors (e.g., thermal stress and ocean acidification) and without intervention, more than 90% of reefs are estimated to be threatened by 2030 (Burke et al., 2011). Balancing the need for benthic ecosystem mapping and acknowledging the complexity of mapping highly heterogeneous benthic ecosystems, the 2017 Decadal Survey of Earth Science recommended the identification and quantification of benthic community structure mapping (pg. 364) with a specific call out to dominant coral reef ecosystem habitats (i.e., coral, algae, sand).  

Thus, this algorithm theoretical basis document describes the algorithm used to derive benthic fractional cover within the L2+ Aquatic Biogeochemistry and Composition section of the SBG-VSWIR aquatic workflow (Figure 1). This type of retrieval falls within shallow water remote sensing, a sub-discipline of aquatic remote sensing that characterizes the influence of benthic reflectance on the reflectance retrieved at the sea surface. Since the bathymetry and water column properties also influences the reflectance retrieved at the sea surface, the bathymetry, water column properties, and benthic reflectance are all defined prior to attributing benthic reflectance to different benthic fractional cover types. We describe a brief history of shallow water remote sensing methods and the derivation of benthic fractional cover from VSWIR remote sensing, and then present the theoretical basis for the SBG Level 2+ algorithm for benthic fractional cover.  

## 3 Context/Background

### 3.1 Historical Perspective
The first studies utilizing VSWIR imaging spectroscopy for shallow water remote sensing arose in the 1990’s (Kutser et al., 2020). With the increased availability of airborne imaging spectrometers, early studies approximated the radiative transfer equation for a water body that is influenced by absorption and backscattering processes within the water column and backscattering from the benthic habitat (Lee et al., 1999; Maritorena et al., 2002). Promising applications to airborne imagery set the stage for scaling shallow water remote sensing with the first civil spaceborne imaging spectrometer, Hyperion on EO-1. Despite being developed for land-based ecosystems, Hyperion’s application to select Australian coral reef ecosystems demonstrated the potential for spaceborne spectrometers to generate benthic maps at global scales. Advances in airborne (AISA, AVIRIS, APEX, CASI, HyMap, HySpex, MIVIS, PHILLS, PRISM, etc.) and spaceborne (e.g., HICO, DESIS, PRISMA) instrumentation further refined algorithm development across coral reef ecosystems; and spurred algorithm development in other benthic ecosystems such as seagrass meadows, kelp beds, and more.  

Benthic fractional cover requires accurate estimations of bathymetry, water column constituents, and benthic reflectance, also called bottom albedo. Bathymetry and water column constituents are key parameters because in accordance with Beer’s Law, reflectance within a scattering and absorbing medium is exponentially attenuated with distance. As a consequence, both complex light interactions within the overlying water column and the bathymetry mediates the retrieval of benthic reflectance, and ultimately, the retrieval of benthic fractional cover. Given the complexities of these derivations, many studies have shown reliable benthic reflectance and benthic fractional cover retrievals in less than 5 meters of water. Water column light interactions within the water column are typically categorized as inherent optical properties (IOPs), the optical properties that do not vary with changing illumination conditions, and apparent optical properties (AOPs), optical properties are sensitive to changing illumination conditions. The bathymetry, benthic reflectance, and water column properties such as IOPs and AOPs have been retrieved from the spectral remote sensing reflectance, Rrs(l), the ratio of water leaving radiance to downwelling irradiance just above the water surface. 

To approximate bathymetric, water column and benthic contributions from Rrs(l), forward and inversion-based modeling have been employed. Forward based bio-optical models (Maritorena et al. 1994) and radiative transfer-based models (Mobley et al. 2003) can be used to generate synthetic Rrs(l) based on varying water column constituents, benthic reflectance, and bathymetry. A sample Rrs(l) can then reference the synthetic Rrs(l) database via spectral matching techniques (i.e., Spectral Angle Mapper, Least Square Minimization) to determine the relative contributions to Rrs(l). These approaches can be used when field measurements may not be available, but it is important that forward based models account for the wide range of absorption and scattering processes shallow water ecosystem may experience.  On the other hand, inversion based methods determine the set of conditions, that is water column constituents, bathymetry, and benthic reflectance, that result in a sample Rrs(l) Types of inversion processes include linear and non-linear optimization (Brando et al. 2009, Lee et al. 1998), and the incorporation of adaptive look up tables (Hedley et al. 2009). Additional studies have refined inversion-based processes through enhancing the benthic classifier (Garcia et al. 2012, 2016) and Bayesian optimization of IOPs and AOPs (Thompson et al. 2017). 

   Spectral mixture analysis methods have been widely used for generating benthic fractional cover maps. Types of methods include linear unmixing (Hochberg and Atkinson, 2003, Hedley et al. 2004, Goodman and Ustin et al. 2007) and first and second spectral derivatives (Bell et al. 2020). The selection of globally representative endmembers of coral, algae, sand, and seagrass is essential for the generation of benthic fractional cover maps.  

  
### 3.2 Additional Information

## 4 Algorithm Description

### 4.1 Scientific Theory

The focus on the L2+ benthic fractional cover product is focused on the identification and quantification of dominant benthic community structures, such as coral, algae, sand, and seagrass. The process in to gather benthic reflectance, inherent optical properties, and bathymetry is based on Thompson et al. 2017 and the simple linear unmixing process with a benthic spectral library are used to generate benthic fractional cover maps (Figure 2).   


#### 4.1.2 Scientific theory assumptions

### 4.2 Mathematical Theory

#### 4.2.1 Mathematical theory assumptions

### 4.3 Algorithm Input Variables

| Name | Long name                     | Unit  |
|------|--------------------------------|-------|
| Rrs  | Remote Sensing Reflectance    | sr⁻¹  |

### 4.4 Algorithm Output Variables

| Name     | Long name                 | Unit |
|----------|---------------------------|---|
| Coral    | Coral Fractinonal Cover   |   |
| Algae    | Algae Fractional Cover    |   |
| Sand     | Sand Fractional Cover     |   |
| Seagrass | Seagrass Fractional Cover |   |

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