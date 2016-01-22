# PANDA (Pipeline for Analyzing braiN Diffusion imAges) #
Pipeline for Analyzing braiN Diffusion imAges (PANDA) is a matlab toolbox for pipeline processing of diffusion MRI images. For each subject, PANDA can provide outputs in 2 types:
  * diffusion parameter data that is ready for statistical analysis (WM atlas-level, voxel-level and TBSS-level);
  * brain anatomical networks constructed by using diffusion tractography (deterministic network: number-weighted, FA-weighted, length-weighted; probabilisitc network: connectivity probability-weighted).

The key advantages of PANDA are as follows:
  * Fully-automatic processing from raw DICOM/NIFTI to final outputs;
  * Supporting both sequential and parallel computation. The parallel environment can be a single desktop with multiple-cores or a computing cluster with a SGE system;
  * A very friendly GUI (graphical user interface).

Some minor advantages of PANDA:
  * If the program terminates mid-way, you can load configuration file and click "RUN", then PANDA will restart from the terminate point;
  * If you change some options, PANDA will only restart the procedures related to these options;
  * The jobs will be run in background, and PANDA & Matlab can be even closed.

PANDA is an open source software. This is a [paper](http://www.frontiersin.org/Human_Neuroscience/10.3389/fnhum.2013.00042/abstract) in Frontiers in Human Neuroscience that provides an overview of PANDA features and implementation. It has been tested under Linux (Ubuntu, Centos, Fedora) and MAC. For PANDA package and manual, please go to [PANDA Website](http://www.nitrc.org/projects/panda/). This project was started in [State Key Laboratory of Cognitive Neuroscience and Learning](http://psychbrain.bnu.edu.cn/), [Beijing Normal University](http://www.bnu.edu.cn/), 2011.

Please report bugs and requests to:
  * Zaixu Cui: zaixucui@gmail.com
  * Suyu Zhong: suyu.zhong@gmail.com
  * [Gaolang Gong (PI)](http://psychbrain.bnu.edu.cn/teachcms/gonggaolang.htm): gaolang.gong@gmail.com

# News #
**June, 1th, 2012 :**

First realease (Version 1.1.0) of PANDA.

**March, 10th, 2013 :**

PANDA 1.2.0 was released.

New features of PANDA 1.2.0 (three parts):

I, new features of **GUI** (graphic user interface):
  * If main window of PANDA is closed, then child windows will be closed automatically;
  * After clicking 'RUN' button, configuration information will be saved to file automatically. The name of the configuration file is "{year}-{month}-{day}-{hour}-{minute}.PANDA", and it will be saved in {Result-Path};
  * A button named "Failed Jobs" is added for viewing the reasons of failed jobs. When some jobs failed, clicking this button, a table with names of failed jobs will come out. Clicking the job in the table, you will see the reason of job failing;
  * There are two modes for monitor table, which are real-time and non-real-time. Default is real-time.  In non-real-time mode, clicking "Refresh" button to update jobs status;
  * Before clicking "RUN" button, if users want to delete a subject from imported raw data, please right click the item of this subject in the Location Table.
  * Supporting csh, tcsh shell environment of linux.

II, **new utilities**:
  * Utility "Brain Extraction (T1)", is for deleting non-brain tissue from T1 image of the whole head. It supports parallel processing for any number of subjects.
  * Utility "Test Bvecs", is for examining whether the direction of the tensor is right. Users can regulate the direction of the tensor, through modifying the parameters "Invert" and "Swap". Whether the direction of the tensor is right determines whether the fiber tracking result is right. It is recommended using this utility to check the direction of the tensor before data analysis, when doing fiber tracking.
  * Utility "Resample NIfTI", is for resampling NIfTI images. It supports parallel processing for any number of subjects.
  * Utility "DICOM->NIfTI", is for converting DICOM files to NIfTI images. It supports parallel processing for any number of subjects.

III, new features for **data analysis**:
  * A .txt file and a .mat file containing subjects' scanning parameters will be produced. If input files are DICOM format, scanning parameters are as follows: "Name", "Sex", "Birth Date", "Scanning Date", "Age", "TR", "TE", "Flip Angle", "Acquisition Matrix", "Slice Thickness", "Spacing Between Slices", "Magnetic Field Strength", "Resolution", "FOV"; If input files are NIfTI format, scanning parameters are as follows: "Quality of voxels", "Resolution", "Quality of volumes", "data type". The file was stored in {Subject-Folder}/quality-control/Scanning-Parameters.
  * An option named "Resampling Resolution" is added in "Diffusion Opt". Users can resample NIfTI images directly converted from DICOM files to a certain resolution. This option is used for set final resolution.
  * Two options named "Invert" and "Swap" are added in "Diffusion Opt". Users should set these two options according to the results of "Test Bvecs" utility or leave them default.
  * The operations in "Diffusion Opt" are optional now.
  * For WM Altas-based results, all subjects' results will be merged to an Excel sheet to make statistical analysis convenient. These Excels are stored in {Result-Path}/Allatlasresults/.
  * For TBSS-based results, all subjects' native skeletons will be merged to 4D data. Following the guidance of FSL website, users can use "randomise" command with this 4D data to do TBSS statistical analysis. These 4D data are stored in {Result-Path}/TBSS/Merged4DSkeleton/.
  * Several operations (Extracting brain, Cropping, Resampling) of T1 images are added in brain parcellation process. In order to do brain parcellation, uses need to input T1 NIfTI images directly converted from DICOM files. In addition, Cropping T1 images is for reducing images size, thus speeding up brain parcellation. T1 images can be resampled to the resolution as "Resampling Resolution" parameter indicates.
  * If brain parcellation is selected, the screenshot of brain parcellation results will be produced, which can be used for examining the results briefly. The screenshot is stored in {Subject-Folder}/quality-control/Individual-Parcellated.
  * An option named "reseed" is added in deterministic fiber tracking, to set the quantity of seeds in each voxel.
  * Two definitions of ROI size are added in network construction: one is ROIVoxelSize,   which is the quantity of voxel in ROI; the other is ROISurfaceSize, which is the quantity of voxel containing the end point of fibers.
  * Some data analysis procedures, such as brain parcellation and probabilistic tracking, are faster than the first version.

# Chinese Version #
http://code.google.com/p/panda-tool/wiki/News_ChineseVersion