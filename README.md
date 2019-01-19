# The Kundaha Project

**WARNING:** Before getting started, please notice Kundaha is **NOT** a clinical software.
It is built for education and demonstration purposes **ONLY**.

The *Kundaha Project* is an initiative for the inclusion of content-based retrieval methods as options for the comparison of diagnosed and undiagnosed medical images.
In this repository, a demonstration tool for mammograms is available (see the *Minimum Requirements* section).
The demonstration enables searching upon 2.892 regions of interest that were acquired from the [DDSM mammogram database](http://marathon.csee.usf.edu/Mammography/Database.html) and manually annotated by an expert following the [BI-RADS standard](https://www.acr.org/).

Our tool was implemented in C++11 standard by using the [QT Cross-Platform API 5.0](https://www.qt.io/), new diversified-based algorithms, and open-source code from our [own GBDI lab](https://bitbucket.com/gbdi/arboretum).

Despite the efforts of the authors to release *Kundaha* without bugs, there may remain some issues.
If you either find an issue or want new features to be added, please *report it*!

**CITATION:** If you want to download and use Kundaha for trials or tech report writing, we kindly ask you to include the following reference.

* Santos, L. F. D; Blanco, G; Oliveira, D.; Traina, A.; Traina Jr., C; Bedo, M. V. N.. *Exploring Diversified Similarity with Kundaha*. CIKM 2018
Proceedings of the 27th ACM International Conference on Information and Knowledge Management (CIKM) 2018: 1903-1906. Torino, Italy, October 22-26, 2018.

See DOI and ACM DL link [here](https://doi.org/10.1145/3269206.3269220).


### 1. Minimum Requirements

* Screen resolution: 1920×1080 (or higher) - Lower resolutions are unsuitable for medical image visualization.
* 8 GB free disk space.
* 4 GB RAM.
* Intel i5 2nd generation core processor.

### 2. Installation

Although Kundaha runs on Windows, Linux-based distributions, and Android, we provide the binary version so that it can be installed without requiring any compilation.

###### 2.1 Windows


To install Kundaha, download the file [*KudanhaInstaller.exe*](https://drive.google.com/file/d/1uMEqR6vDkCdtjhddGpwMHbu10zj7QYq-/view?usp=sharing) (link redirects to Google Drive*) and be sure of using an environment as described in the *Minimum Requirements* section.
After downloading the installer, please select the directory to be used for the installation (the default location is a new directory named Kundaha at the root of the OS file system).
A link to Kundaha will be added to your desktop.

*Binary installer file exceeds GitHub maximum allowed file size.

![Kundaha Windows](/readme_images/kundaha_windows.png)

###### 2.2 Linux-based distributions (requires Wine)

Before starting, be sure [Wine](https://www.winehq.org/) application is installed into your Linux distribution.
Next, download the Kundaha file [*Kundaha4Wine.zip*](https://drive.google.com/file/d/1HkHa7HqeTxQjc2gOZ0JqJdyDqxJa_EKI/view?usp=sharing) (link redirects to Google Drive*).
Unpack Kundaha4Wine.tar.gz at the directory of your preference.
Start Wine on Kundaha.exe to run the demonstration.

*Compressed file exceeds GitHub maximum allowed file size.

### 3. Using Kundaha

Launch the Kundaha desktop application for searching.
The demonstration first screen is a pool list of undiagnosed images to be queried.
The idea is experts may crop regions of interest from large studies and put them into a list for further
analyses.

There is an example of an image to be queried, but you may include an image to be queried by your
own (see *Including a Query Element* section).

Please, see this [Youtube video](https://www.youtube.com/watch?v=yOxvUVuQAbk) for an example of Kundaha usage.

###### 3.1 Search Parameters

There are seven image descriptors available that represent low-level features of color, texture, and shape.
Additionally, there are five distance functions that can be used to measure the similarity between the query element and the images in the dataset.

###### 3.2 Similarity Queries and its Features

After selecting *similarity* as the search criterion, Kundaha performs a standard similarity search and presents the result set as a new screen.

* Putting the mouse upon an image of the result set enables the visualization of the annotation related to that specific result.
* Double-clicking brings the image from the result set to the center of the window.
* At the center of the window, the image can be enlarged and you can employ a high-contrast windowing operation for a better visualization.
* Left-click triggers the exclusion of an image in the result set that is not relevant.
* Right-click enables you to mark an image in the result set as relevant.
* After labeling relevant and non-relevant images, you may request Rocchio-based relevance feedback cycles to explore more similar images.

###### 3.3 Diversified Similarity Queries and its Features

After selecting *diversity* as the search criterion, Kundaha performs a diversified similarity search and presents the result set as a new screen.

* The representative images from strong influence sets are displayed on the right.
* Right-click expands and collapses a strong influence set.
* The list of representatives enables a result exploration from a diversity perspective, whereas the influence sets are kept sorted by similarity. Therefore, you can easily shift the exploration perspective from diversity to similarity.
* If an image is labeled as relevant, it is permanently kept in the "My List of Relevant Images" until you explicitly remove it.
* Images of strong influence sets can be dismissed with left-clicks. The entire influence set is dismissed if you discard the representative.
* Images labeled as relevant are kept in the "My List of Relevant Images".
* Diversified relevance feedback cycles shift the positioning of the query element by using the size of strong influence sets as another weight in the Rocchio-based relevant feedback algorithm.
* For each relevance feedback cycle, the retrieved images in the result set can be compared to others previously included in the "My List of Relevant Images".


### 4. Including a Query Element

You may include a region of interest from a mammogram to be queried by your own.
This [Youtube link](https://www.youtube.com/watch?v=2LOD-JF7WDQ) describes how to upload a query element to Kundaha.

Medical images are usually high-contrast DICOM files and they are visualized through proper DICOM Viewers.
Such tools enable the cropping of regions of interest that can be straightforwardly uploaded to Kundaha.
However, you can also upload a region of interest based on regular .bmp, .jpg, or .png file formats that you may have cropped from the image editor of your preference.
The difference, in this case, you'll not be allowed to perform windowing operations in your query element due to the absence of high-contrast.

In this repository, we provide two other examples of regions of interest.
The examples are located in the directory */examples* (files [*query_example_2.krl*](examples/query_example_2.krl) and [*query_example_3.jpg*](examples/query_example_3.jpg*)).
As a suggestion, other regions of interest can be extracted from the [DDSM repository](http://marathon.csee.usf.edu/Mammography/Database.html).

### 5. Search Parameters

Tuning search parameters for the retrieval of regions of interest from mammograms also depend on the users' query hypothesis.
In fact, some combinations of *feature extractor* and *distance function* (*image descriptors*, for short) are more suitable for the retrieval of images related to certain query hypothesis than others.
In the mammogram dataset of our example, we have multiple labels for the same ROI.
For instance, the ROI may present malign mass and benignant calcification at the same time.
Although there is no requirement for such, the following image descriptors achieved the best Precision for most of Recall values regarding fixed query hypotheses in our empirical experiments:

* BIC extrator and Euclidean distance: No query hypothesis
* Haralick and City-Block distance: Mass hypothesis
* Normalized Histogram/LBP and Canberra: Calcification hypothesis

### 6. Additional Information and Legal Note

*Demonstration binary file is under LGPL-3 constraints due to the free use of the QT API 5.0 requirements*.

*The demonstration is provided 'as is' and any expressed or implied warranties, including but not limited to, the implied warranties of merchantability and fitness for a particular purpose are disclaimed.
In no event shall the authors of this software or its contributors be liable for any direct, indirect, incidental, special, exemplary, or consequential damages (including but not limited to, procurement of substitutive goods or services, loss of use, data, or profits; or business interruption) however caused and on any theory of liability wheter in contract, strict liability, or tort (including negligence or otherwise) arising in any way out of the use of this demonstration, even if advised of the possibility of such damage.*

Again, Kundaha is **NOT** a clinical software.
