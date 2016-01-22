# News #
**2012年6月1日：**

第一个版本 PANDA 1.1.0 发布。

**2013年3月10日：**

第二个版本 PANDA 1.2.0 发布。

PANDA 1.2.0 新增的功能（三个部分）：

I, GUI（图形用户接口）的新特征：
  * 关闭PANDA的主窗口，子窗口也会随之关闭。
  * 用户点击"RUN"按钮之后，配置信息会自动保存到文件中，配置文件的命名为"{year}-{month}-{day}-{hour}-{minute}.PANDA", 它将存放在{Result-Path}路径下；
  * 界面中添加了名字为"Failed Jobs"的按钮，用于查看作业失败的原因。如果monitor table中显示作业failed，点击这个按钮，弹出的界面会在table中显示失败的作业的名字，点击table中的某个作业，可以查看到该作业失败的原因。
  * 现在，monitor table有两种显示模式：实时和非实时。默认是实时。在非实时模式下，点击"Refresh"按钮可以更新作业的状态。
  * 在点击"RUN"按钮之前，如果用户想从导入的输入数据中删除某被试，只要在Location Table中右键点击该被试所在行。
  * 现在也支持csh, tcsh的shell环境。

II, 新的子工具
  * 工具Brain Extraction (T1), 用来对T1数据剥头皮，可以并行、批处理。
  * 工具Test Bvecs, 用于检测拟合得到的张量方向是否正确。用户可以修改该中介下的"Invert"和"Swap"两个参数来调节拟合得到的张量方向。由于张量方向的准确与否决定了纤维追踪结果的正确与否，所以建议用户在进行纤维追踪之前，先利用这个工具，检查生成的张量方向。
  * 工具Resample NIfTI, 用来对NIfTI图像重采样，可以并行、批处理。
  * 工具DICOM->NIfTI, 用来将DICOM图像转换成NIfTI图像，可以并行、批处理。

III, 用于数据分析的功能
  * 为每个被试生成一个.txt文件和.mat文件，存放该被试的扫描参数。如果输入时DICOM文件，扫描参数如下：名字、性别、出生日期、扫描日期、年龄、TR、TE、Flip Angle、Acquisition Matrix、层厚、层间距、场强、分辨率、FOV；如果输入时NIfTI文件，扫描参数如下：图像大小、分辨率、volume的数量、数据类型。结果存放在{Subject-Folder}/quality-control/Scanning-Parameters路径下。
  * 在Diffusion Opt中加入了Resampling Resolution的参数。用户可以在进行一系列分析之前，先对原始DICOM转换得到的NIfTI图像重采样，这里设置的是重采样的分辨率。
  * 在Diffusion Opt中加入了Invert和Swap两个参数。用户根据Test Bvecs工具得到的正确的Invert和Swap，来设置这里的两个参数。
  * 在Diffusion Opt中包含了dMRI数据的基本的几种分析，用户可以选择哪些做，哪些不做。
  * 基于atlas的分析结果，软件会将所有被试的结果合成一个大的Excel以方便统计分析。结果存放在{Result-Path}/Allatlasresults/路径下。
  * 基于TBSS的分析结果，所有被试的个体空间的骨架会合并成一个4D的数据。按照FSL网站的指导，用户可以用这个4D的数据做输入，使用randomise命令进行统计分析。这些4D数据存放在{Result-Path}/TBSS/Merged4DSkeleton/路径下。
  * 脑区分割中加入了对T1图像剥头皮、cropping、重采样的操作。所以，用户只要输入直接由DICOM转换得到的T1的NIfTI图像就可以，设置剥头皮的参数，PANDA会对T1剥头皮。Cropping操作可以对图像截取，使脑区分割加速。如果需要对T1图像重采样，可以设置重采样分辨率。
  * 如果做脑区分割，在{Subject-Folder}/quality-control/Individual-Parcellated路径下会生成脑区分割结果图像的截图，用户可以大致看一下分割结果。
  * Deterministic Fiber Tracking中加入了reseed的参数，设置每个voxel内种子点的数量。
  * 网络构建中增加了两个ROI大小的定义：第一个是ROIVoxelSize，即ROI内voxel的数量；第二个是ROISurfaceSize，即ROI内含有纤维终点的voxel的数量。
  * 一些流程，比如脑区分割、概率追踪，都比第一个版本更快了。