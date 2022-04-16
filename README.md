# Test torchserve with Mnist 


### Usage

- Step 1: Create a torch model archive using the torch-model-archiver utility to archive the above files.
```commandline
torch-model-archiver --model-name mnist --version 1.0 --model-file ./mnist.py --serialized-file ./models/mnist_cnn.pt --handler  ./mnist_handler.py
```

- Step 2: [Optional] Perform this step to use pytorch profiler. Set the following environment variable
```commandline
export ENABLE_TORCH_PROFILER=true
```

- Step 3: Register the model on TorchServe using the above model archive file and run digit recognition inference
```commandline
mkdir model_store

mv mnist.mar model_store/

torchserve --start --model-store model_store --models mnist=mnist.mar --ts-config config.properties

curl http://127.0.0.1:8080/predictions/mnist -T ./test_data/0.png
```
