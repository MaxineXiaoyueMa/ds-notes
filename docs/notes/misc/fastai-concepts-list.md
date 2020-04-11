concept notes for fastai
> laundry list note from fastai classes with supplemental information
> most example codes are from the fast.ai notebooks
>

## fasiai library
- fastai.datasets.untar_data(): download file to some convenient path, untar it, return the value of path
`path = untar_data(URLs.PETS); path`
fastai.vision.data()

- get_image_files(path_to_image):grab an array of image files based on extension in a path
```python
fnames = get_image_files(path_to_image)
fnames[:5]
```
```python
[PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/american_bulldog_146.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/german_shorthaired_137.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/japanese_chin_139.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/great_pyrenees_121.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/Bombay_151.jpg')]
 ```
- DataBunch: general fastai concept for data, subclasses include ImageDataBunch, contains 2 or 3 datasets(train/val/(test)), each dataset contains images/texts/tabular data and labels
 - `ImageDataBunch`: object,
   - `ImageDataBunch.from_name_re`: method that extracts labels from the names
   - `data = ImageDataBunch.from_name_re(path_img, fnames, pat, ds_tfms=get_transforms(), size=224, bs=bs)`
      path_img: a path containing images
      fnames: a list of file names
      pat: a regular expression (i.e. pattern) to be used to extract the label from the file name
      ds_tfm: we'll talk about transforms later
      size: what size images do you want to work with.
      bs: batch size (i.e. number of images processed at a time). Currently, 64, Set to 16 if memory is not enough.
    - `data.normalize(imagenet_stats)`: all data about the same size
    - `data.show_batch(rows = 3, figsize = (7,6))`: watch for borders, texts, odd rotation
    - `data.classes`: all possible label names

- Learner: general concept for things that can learn to fit a model, subclasses include convnet learner that can create a convolutional neural network
  - `learn = cnn_learner(data, models.resnet34, metric = error_rate)` : data = a data bunch, arch = architecture, metrics is what you want to print out while training
  - `learn.fit_one_cycle(1)`: add a few extra layers to the end, and only train those
  - `learn.save('stage-1')`: save the weights names stage-1
  - `learn.unfreeze()`: train the whole model
  - `learn.load('stage-1')`: load the weights form before
  - `learn.lr_find()`: how fast can I train without overshooting

- class interpretation
  - `interp = ClassificationInterpretation.from_learner(learn)`
  - `interp.plot_top_losses(9, figsize=(15,11))`
  - `interp.most_confused(min_val=2)`

## python modules
### pathlib
- `import pathlib`
- path = PosixPath('foo/bar')
- `path.ls()`:
  [PosixPath('/home/data/annotations'),
  PosixPath('/home/data/images')]
- new_path = path/'annotations'

### re
