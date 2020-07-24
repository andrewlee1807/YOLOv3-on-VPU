# YOLOv3-on-VPU
<h1> Configured and run Yolov3 model test on COCO </h1>
<h2> Functions Utils: <h2>
1. Convert .weight to .H5 <br/>
2. Convert .weight to .PB <br/>
3. Check graph base on .PB model file <br/>
<h2>Note:<h2><br/>
  - This's project runs on windows 10. <br/>
  - Cause YOLO's architecture some layers are not support run on VPU, so we have to exit from YOLOv3 with 3 outputs, then ParseYOLOV3Output helps to combine to get the final result.<br/>
  
![Optional Text](../main/Yolo_architecture.PNG)

  - yolo_v3.json is cfg file that is used by converting to IR type 
  - "ParseYOLOV3Output" is the same function "_detection_layer".<br/>
  To get the graph of YOLO, run: <br/>
  
```python
> python checkgraph.py
> tensorboard --logdir
 ```
 - Convert PB to IR model : <br/>
 python mo_tf.py --input_model "Inference YOLOv3 COCO\frozen_darknet_yolov3_model_PINTO.pb" --output_dir "C:\Users\BlackHole\Desktop" --tensorflow_use_custom_operations_config "extensions/front/tf/yolo_v3.json" --batch 1  --data_type FP16<br/>
 - Starting inference : <br/>
 
 ```python
 > python Inference_VPU.py
 ```
 # Requirement :<br/>
 - Installed python3, Openvino.
  <p>References : PINTO</p>
  <a>https://github.com/PINTO0309/OpenVINO-YoloV3/blob/master/pbmodels/download_yolov3.sh</a>

