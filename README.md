# Benchmark_Model_inference
Image Classification Models Supported by TensorRT Server (Triton Server):

resnet10/resnet18/resnet34/resnet50/resnet101
vgg16/vgg19
googlenet
mobilenet_v1/mobilenet_v2
squeezenet
darknet19/darknet53
efficientnet_b0
cspdarknet19/cspdarknet53


In this project we will be benchmarking deep learning inference. 

Particularly we will be examining the performance of our deep learning models  hosted on cloud while performing inferences with various batch sizes.

Our deep learning models are hosted on an AWS EC2 instance.

To get us started, we will need to create **_p3.2large_** ec2 instance with NVIDIA Deep learning AMI.


A **p3.2large** ec2 instance will have the following specifications:
1) One NVIDIA Tesla V100 GPU
2) High frequency Intel Xeon E5-2686 v4 processor 
3) 61 GiB memory
4) 16 GiB GPU memory

You are free to select instances with more than 1 NVIDIA GPU.

Now once we have our EC2 instance up and running we will proceed to pull Triton Inference server container in our instance using docker with the following command.

Install docker
sudo yum install docker
sudo systemctl start docker

**$ docker pull nvcr.io/nvidia/tritonserver:22.03-py3**

sudo docker run --rm -p8000:8000 -p8001:8001 -p8002:8002 nvcr.io/nvidia/tritonserver:22.03-py3 tritonserver --model-repository=s3://modelsyppatel/model_repository

Get Client Libraries
docker pull nvcr.io/nvidia/tritonserver:22.03-py3-sdk
docker run -it --rm --net=host nvcr.io/nvidia/tritonserver:22.03-py3-sdk
/workspace/install/bin/image_client -m inception_graphdef -c 3 -s INCEPTION /workspace/images/mug.jpg