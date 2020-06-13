# facenet models

This is a convenience package for making available [facenet-pytorch](https://github.com/timesler/facenet-pytorch)'s trained face recognition model, which achieves state-of-the-art face recognition results.

## Installation instructions 

### Non-Anaconda Instructions

Install OpenCV:

```
pip install opencv-python
```

then install facenet-pytorch:

```
pip install facenet-pytorch
```

Clone facenet_models, navigate to the resulting directory, and run

```
python setup.py develop
```

### Anaconda Instructions

First, create and switch to a new environment.

```
conda create -n facenet
conda activate facenet
```

Install numpy, matplotlib, and jupyter:

```
conda install numpy matplotlib jupyter
```

Next, install PyTorch. 
We use the CPU-only version, but if you have a GPU you want to use and you don't mind some extra work to use it, you can find installation instructions [here](https://pytorch.org).
All included code should be compatible with the CUDA versions of PyTorch, but we make no guarantees.

Windows and Linux installation:
```
conda install pytorch torchvision cpuonly -c pytorch
```

MacOS installation:
```
conda install pytorch torchvision -c pytorch
```

Next, install [OpenCV and the Camera package](https://github.com/cogworksbwsi/camera) by following the instructions in that repo.

Install facenet-pytorch:
```
pip install facenet-pytorch
```

Finally, clone this repo, navigate into it, and run
```
python setup.py develop
```

## Usage

``` python
from facenet_models import FacenetModel

# this will download the pretrained weights (if they haven't already been fetched)
# which should take just a few seconds
model = FacenetModel()

# detect all faces in an image
# returns a tuple of (boxes, probabilities, landmarks)
# assumes ``pic`` is a numpy array of shape (R, C, 3) (RGB is the last dimension)
boxes, probabilities, landmarks = model.detect(pic)

# producing a face descriptor for each face
# returns a (N, 512) array, where N is the number of boxes
# and each descriptor vector is 512-dimensional
descriptors = model.compute_descriptors(pic, boxes)
```

## Documentation for facnet_models

```
detect(image)

Detect faces in an image.

Parameters
----------
image : np.ndarray, shape=(R, C, 3)
    The image in which to detect faces.

Returns
-------
Tuple[np.ndarray shape=(N, 4), np.ndarray shape=(N,), np.ndarray shape=(N, 5)]
    (boxes, probabilities, landmarks) where:
    - boxes is a shape-(N, 4) array of boxes, where N is the number of faces detected in the image.
    - probabilities is a shape-(N,) array of probabilities corresponding to each detected face.
    - landmarks is a shape-(N, 5) arrays of facial landmarks corresponding to each detected face.



compute_descriptors(image, boxes)

Compute descriptor vectors for the faces contained in ``boxes``.

Parameters
----------
image : np.ndarray, shape=(R, C, 3)
    The image in which to detect faces.

boxes : np.ndarray, shape=(N, 4)
    The bounding boxes containing the faces for which to compute descriptors.

Returns
-------
np.ndarray, shape=(N, 128)
    The descriptor vectors, where N is the number of faces.
"""
```
