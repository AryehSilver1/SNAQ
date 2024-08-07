## SNAQ: Spatial Neighborhood Analysis of QuPath

### Introduction
SNAQ provides tools for analyzing immunohistochemically stained tissue samples at the single-cell level, focusing on spatial patterns and cellular interactions.

### Table of Contents
1. [Description](#description)
2. [Background](#background)
3. [Methods](#methods)
4. [README For "Data Analysis.Rmd"](#readme-for-data-analysisrmd)
   - [Setup](#setup)
   - [Configuration](#configuration)
   - [Running the Analysis](#running-the-analysis)
   - [Output](#output)
5. [README for "Plot Maker.Rmd"](#readme-for-plot-makerrmd)
   - [Data Initialization](#Data-Initialization)
   - [Data Combining and Analysis](#Data-Combining-and-Analysis)
   - [Plot Descriptions and Instructions](#Plot-Descriptions-and-Instructions)
   - [Output](#output)
6. [Running the Test Data](#running-the-test-data)
   

## Description
The R Markdown document titled "Template Data Analysis" automates the analysis of immunohistochemically stained tissue samples at the single-cell level using RStudio. The primary focus is on neighborhood analysis of cellular interactions within fluorescently stained samples. The methodology integrates image processing, cellular classification, and geospatial analysis to identify and visualize spatial patterns of different cell types and their proliferation markers.

## Background
Analyzing the local microenvironment around tumor cells can provide crucial insights into the interactions between tumor and immune cells. This document provides a framework to quantify these interactions by analyzing the distances between cell types within specified radii and visualizing these relationships.

## Methods
1. **Image Acquisition**: Fluorescent images are acquired using a fluorescent microscope.
2. **Data Classification in QuPath**: Cells are detected and classified into types based on their staining markers. Data is exported as CSV files for each image. Refer to the paper for specifics on how to process images using QuPath.
3. **R Analysis**: The R script processes image data in bulk to analyze the neighborhood relationships between cells using distances calculated from their coordinates.


### Below is a detailed explanation of the usage of two R scripts: `Data Analysis.Rmd` and `Plot Maker.Rmd`. Each README provides comprehensive instructions on setup, configuration, running the analysis, and understanding the outputs, ensuring a clear and efficient workflow for users.


## README For "Data Analysis.Rmd"

## Setup
1. **Install R and RStudio**: Ensure you have R and RStudio installed on your system. You can download them from [CRAN](https://cran.r-project.org) and [RStudio's website](https://rstudio.com/products/rstudio/download/), respectively.

2. **Install Required Packages**: Open RStudio and install the required libraries by running:
   ```R
   install.packages(c("readxl", "tidyverse", "data.table", "foreach", "doParallel"))
   ```

3. **Data Preparation**: Import data from QuPath into R Studio by running the "Importing data table" code chunk.<br>NOTE: If your images are from a larger stitch, run the code chunk labeled "Separates the full data CSV file into separate CSV files for each ROI" and fill in the information for the ROI centroid locations before loading in your data

## Configuration
- Modify the variable section to match your dataset specifics, including:
  - `dist1`, `dist2`, `dist3`: Distances for the radius of each concentric ring (smallest to largest).
  - `maxXum`, `maxYum`: Image dimensions in microns.
  - `numImages`: Total number of images to analyze.
  - `markerA`, `markerB`, `markerC`: Markers to analyze.
  - `inputFolder`, `outputFolder`: Directories for input and output data.
    
### Marker Types
- **Marker A**: Represents a specific cell type A.
- **Marker B**: Represents a specific cell type B.
- **Marker C**: Represents a modifier marker that can modify Marker B.

### Marker Interactions
- **Marker C modifies Marker B**: Only Marker C can modify Marker B. This interaction is a key aspect of the analysis.

## Running the Analysis
1. Load the R Markdown file in RStudio.
2. Set your working directory to the directory containing your data and script:
   ```R
   setwd("your/directory/path")
   ```
3. Run the script by knitting the document in RStudio.

## Output
- The output will be generated in the specified output directory and will include Neighbourhood analysis results based on the defined parameters.




## README for "Plot Maker.Rmd"

**Install Required Packages**: Open RStudio and install the required libraries by running:
   ```R
   install.packages(c("readxl", "tidyverse", "ggsignif", "ggdark", "data.table", "ggthemes"))
   ```

Ensure all these packages are installed and loaded as indicated in your R script to handle data manipulation and plotting tasks efficiently.

## Data Initialization
Variables such as `dist1`, `dist2`, `dist3` (distances for measurement rings), `maxXum`, `maxYum` (image dimensions), and `numberOfImages` are set up at the beginning of the script. Adjust these variables according to your dataset specifics, ensuring they remain the same as in "data analysis.rmd".

## Data Combining and Analysis
The script offers functionality for:
- **Combining all images into one dataframe**: Aggregating data from multiple CSV files into a single data frame for comprehensive analysis.
- **Analyzing one image at a time**: Focusing on data from a single image for detailed analysis.

## Plot Descriptions and Instructions

### Three Concentric Rings Plot
- **Description**: Visualizes the proportion of different cellular markers within three concentric rings around each cell type, with each ring representing a specific radius.
- **Instructions**:
  - Prepare data including measurements for each cell type.
  - Run the plotting code section from the R Markdown that corresponds to the Three Rings visualization.
  - Customize plot aesthetics such as colors and labels to fit your presentation needs.
 
<img  src = "https://github.com/avinashpittu/Methods/assets/168061558/ef0b40e8-17db-4eee-9b56-4df08ca805a3" alt = "Concentric Rings" width = "382"/>


### Cell Grid Plot
- **Description**: Shows the spatial arrangement of cells on a grid based on their coordinates within a tissue sample, ideal for a single image analysis.
- **Instructions**:
  - Ensure data includes coordinates and cell type markers.
  - Run the relevant code section for generating the cell grid plot.
  - Adjust visualization parameters to enhance clarity and insight.

### C+ Cell Count Bar Graph
- **Description**: Displays counts of C+ and C- cells across different cell types using a bar graph.
- **Instructions**:
  - Confirm that data columns correctly indicate C+ status.
  - Execute the bar graph plotting code provided in the R Markdown.
  - Modify the bar colors and labels to ensure readability.

### Distance to Closest Cell Control Plot
- **Description**: Evaluate the minimum distance from each macrophage to the closest cell, highlighting macrophage isolation or clustering.
- **Instructions**:
  - Data must include `x` and `y` coordinates and cell types.
  - Calculate distances and generate the plot using the plotting code.
  - Customize the plot to reflect the specific characteristics of your analysis.

### Opposite Average Distance Plot
- **Description**: Calculates and visualizes the average distance of the closest cells of type B from every cell of types A or D.
- **Instructions**:
  - Prepare data with necessary coordinates and cell types.
  - Run the average distance calculation and visualization code.
  - Choose appropriate colors and adjust labels for clear data presentation.

## Output
The outputs include various plots and visualizations that provide insights into cellular interactions and spatial distributions within the tissue sample. Each plot helps in understanding different aspects of the cellular environment, aiding in scientific analysis and research dissemination.

## Running the Test Data

Within both `Data Analysis.Rmd` and `Plot Maker.Rmd`, the variables required for user input are pre-set for the test data. Follow these steps to run the test data:

1. **Download Test Data**:
   - Download `PDAC_measurements.csv` from the Input folder.

2. **Data Analysis Setup**:
   - Direct the `inputFolder` path within `Data Analysis.Rmd` to the location where `PDAC_measurements.csv` is saved:
     ```r
     inputFolder <- "path/to/your/input/folder"
     ```
   - Change the `outputFolder` variable to the path where the output Excel files will be deposited:
     ```r
     outputFolder <- "path/to/your/output/folder"
     ```

3. **Plot Maker Setup**:
   - Set the `inputFolder` variable in `Plot Maker.Rmd` to the path where the output from `Data Analysis.Rmd` was saved:
     ```r
     inputFolder <- "path/to/data/analysis/output"
     ```
   - Set the `outputFolder` variable in `Plot Maker.Rmd` to the path where the images of the data visualizations will be deposited:
     ```r
     outputFolder <- "path/to/your/plot/output/folder"
     ```
   
Ensure that these paths are correctly set in both R Markdown files before running the analysis and generating plots.

---
