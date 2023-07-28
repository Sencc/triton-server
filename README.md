# triton server with SAM

This is an example of deploying a segment anything model using triton server.

# 1.Install the triton server

Refer to https://github.com/triton-inference-server/server

```sh
# use docker
docker pull nvcr.io/nvidia/tritonserver:23.06-py3
```

# 2.Export onnx for sam

This is my exported onnx model,It's divided into encoder and decoder, which can be downloaded from Google Web Drive.

```sh
# encoder
https://drive.google.com/file/d/1612aC4Fd8jrIxZo1xzJi9O3bj61D3ayS/view?usp=sharing
https://drive.google.com/file/d/1AdJ8j0JROmMr1EplPh233rO2GNbFKjRm/view?usp=sharing

# decoder
https://drive.google.com/file/d/1nkI3qJQORQM6Vid4rSOuxmyw0EIzMBDT/view?usp=sharing

# mv .onnx to ./docs/examples/model_repository/sam_encoder_onnx/1 

```



# 3.Run docker

```sh
cd ./docs/examples

docker run --gpus all -itd --rm --name triton_server --net host --shm-size=4g -p8000:8000 -p8001:8001 -p8002:8002 -v $PWD:/workspace/triton_examples nvcr.io/nvidia/tritonserver:23.06-py3

# container
cd /workspace/triton_examples
tritonserver --model-repository ./model_repository

```



# 4.Grpc client