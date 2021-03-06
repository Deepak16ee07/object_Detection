



## How to Run

Easy way: run [this Colab Notebook](https://colab.research.google.com/drive/1s6voDlOGC9m9jtwmcyVl1JchHfxHfJZf?usp=sharing).

Alternatively, if you want to use your images instead of ones comes with this repo.

Require [Python 3.5+](https://www.python.org/ftp/python/3.6.4/python-3.6.4.exe) installed.
### Fork and clone this repository to your local machine.
```
https://github.com/Deepak16ee07/object_Detection
```
### Install required libraries
`pip3 install -r requirements.txt`


### Step 1: Annotate some images
- Save some photos with your custom object(s), ideally with `jpg` extension to `./data/raw` directory. (If your objects are simple like ones come with this repo, 20 images can be enough.)
- Resize those photo to uniformed size. e.g. `(800, 600)` with
```
python resize_images.py --raw-dir ./data/raw --save-dir ./data/images --ext jpg --target-size "(800, 600)"
```
Resized images locate in `./data/images/`
- Train/test split those files into two directories, `./data/images/train` and `./data/images/test`

- Annotate resized images with [labelImg](https://tzutalin.github.io/labelImg/), generate `xml` files inside `./data/images/train` and `./data/images/test` folders. 

*Tips: use shortcuts (`w`: draw box, `d`: next file, `a`: previous file, etc.) to accelerate the annotation.*

- Commit and push your annotated images and xml files (`./data/images/train` and `./data/images/test`) to your forked repository.
## add the zip file of the labeled dataset to the repository

### Step 2: Open [Colab notebook](https://colab.research.google.com/drive/1qhjuSbT4DWw-vZ3z40cHXNGUus_fXQED?usp=sharing)
- Replace the repository's url to yours and run it.

### For Converting the (.xml to .csv) , (.csv to .tfrecord) and to create tabel_map.pbtext file 
```
https://github.com/De%cd {repo_dir_path}

# Convert train folder annotation xml files to a single csv file,
# generate the `label_map.pbtxt` file to `data/` directory as well.
!python xml_to_csv.py -i data/images/train -o data/annotations/train_labels.csv -l data/annotations

# Convert test folder annotation xml files to a single csv.
!python xml_to_csv.py -i data/images/test -o data/annotations/test_labels.csv

# Generate `train.record`
!python generate_tfrecord.py --csv_input=data/annotations/train_labels.csv --output_path=data/annotations/train.record --img_path=data/images/train --label_map data/annotations/label_map.pbtxt

# Generate `test.record`
!python generate_tfrecord.py --csv_input=data/annotations/test_labels.csv --output_path=data/annotations/test.record --img_path=data/images/test --label_map data/annotations/label_map.pbtxtepak16ee07/object_Detection
```



## How to run inference on frozen TensorFlow graph

Requirements:
- `frozen_inference_graph.pb` Frozen TensorFlow object detection model downloaded from Colab after training. 
- `label_map.pbtxt` File used to map correct name for predicted class index downloaded from Colab after training.

You can also opt to download my [copy](https://github.com/Tony607/object_detection_demo/releases/download/V0.1/checkpoint.zip) of those files from the GitHub Release page.


Run the following Jupyter notebook locally.
```
local_inference_test.ipynb
```


