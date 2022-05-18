# Using the Stereolab ZED 2 streams with Nvidia Deepstream YOLO gstreamer pipline examples
 
Here are some gstreamer pipelines that you can use to get the video stream from a ZED 2 camera
 and use it with nvidia Deepstream. This uses the Deepstream YOLO example.
 
 Here is link to a video that gives explanation on how to do it
 
 https://youtu.be/w4VuFPR5F9w
 
 Link to Stereo lab gstreamer github repo
 
 https://github.com/stereolabs/zed-gstreamer
 
 link to Nvidia Deepstream install for jetson
 
 https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Quickstart.html#jetson-setup
 
 
 ZED2 Left image & YOLO Deepstream 6.0.1
 
gst-launch-1.0 zedsrc stream-type=0 ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0

ZED2 Right image & YOLO Deepstream 6.0.1

gst-launch-1.0 zedsrc stream-type=1 ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0

ZED2 Stereo image & YOLO Deepstream 6.0.1

gst-launch-1.0 zedsrc stream-type=2 ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0

ZED2 Depth image & YOLO Deepstream 6.0.1

gst-launch-1.0 zedsrc stream-type=3 ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0

ZED2 Left & Depth image & YOLO Deepstream 6.0.1

gst-launch-1.0 zedsrc stream-type=4 ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0

ZED2 using both Nvidia YOLO deepstream model and ZED object reconition model at the same time

gst-launch-1.0 zedsrc stream-type=0 od-enabled=true od-detection-model=0 camera-resolution=2 camera-fps=30 ! zedodoverlay ! videoconvert ! 'video/x-raw,format=(string)YUY2' ! nvvidconv ! 'video/x-raw(memory:NVMM),format=(string)NV12,width=1280,height=720' ! nvvidconv ! mux.sink_0 nvstreammux live-source=1 name=mux batch-size=1 width=1280 height=720 ! nvinfer config-file-path=/opt/nvidia/deepstream/deepstream-6.0/sources/objectDetector_Yolo/config_infer_primary_yoloV3.txt ! nvvideoconvert ! nvdsosd ! nvegltransform ! nveglglessink sync=0
