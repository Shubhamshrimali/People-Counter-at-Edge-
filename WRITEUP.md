# Project Write-Up
In this project i used RCNN model. It has 0.4 probability threshold. It is have high acuracy. Sometime it get delay when box arounf picture not appear. Interfernce is easy and understood.

wget http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
tar -xvf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
cd faster_rcnn_inception_v2_coco_2018_01_28
python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --reverse_input_channels --tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/faster_rcnn_support.json

## Explaining Custom Layers
Custom layers are layers that are not in the supported list of layers of OpenVino. The list of supported layer is different for each framework, such as Tensorflow, PyTorch, and Caffe. There are situations where the model we would like to use may include such layers, so it is important to be able to handle them. The handling of custom layers is different for each deep learning framework. Details about that can be found over at the OpenVino documentation.

## Comparing Model Performance

Comparison	Inference Time (per frame in ms)	Model Size (Mb)
Faster-RCNN (pure tensorflow)	1222	523
Faster_RCNN (after conversion with the inference engine)	991	311

## Assess Model Use Cases
A possible use case for the people counter app is for instance in the entrance of a place like a swimming pool. The app will be automatically counting how many people enter and leave the place, giving us the number of people inside and thus warning when the capacity for the pool is reached. An application like that removes the need for a person to be there to actually count the people manually.

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. Bad lighting or very bright one can both cause difficulty in the inference of the model. The better lighting and quality available the higher accuracy we can achieve, with possible higher cost for the hardware used.

## Model Research

[This heading is only required if a suitable model was not found after trying out at least three
different models. However, you may also use this heading to detail how you converted 
a successful model.]

In investigating potential people counter models, I tried each of the following three models:

- Model 1: [SSD Mobilenet]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments
  - python mo_tf.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --re
