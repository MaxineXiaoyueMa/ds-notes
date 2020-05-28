# concept notes for fastai
> laundry list note from fastai classes with supplemental information
> most example codes are from the fast.ai notebooks

## fasiai library
### download data, sample data
#### sample data
- image: `path = untar_data(URLs.PETS)`
- nlp: `path = untar_data(URLs.IMDB_SAMPLE)`

- fastai.datasets.untar_data(): download file to some convenient path, untar it, return the value of path
`path = untar_data(URLs.PETS); path`
`path = untar_data(URLs.IMDB_SAMPLE)`
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

### DataBunch
DataBunch: general fastai concept for data, subclasses include ImageDataBunch, contains 2 or 3 datasets(train/val/(test)), each dataset contains images/texts/tabular data and labels
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

## Natural Language Processing (NLP tasks) - Week 4
**Transfer learning for NLP tasks starts with a language model: pre trained model Wikitext 103, then fine tune within interested domain (self supervised learning), finally apply to specific tasks.**
For example, fine tune with movie reviews, model learns 'reviews and what reviews describe', which then help with sentiment analysis

- **Language Model**: predict what the next word is in a sentence, e.g., 'auto complete'
- **Wikitext 103**: subset of most of the largest articles from Wikipedia, 1 billion tokens, model learns 'language and what language describes'

### fastai NLP basic process
- import module: `from fastai.text import *`
- download data:
    - nlp sample, imdb 10k sample: `path = untar_data(URLs.IMDB_SAMPLE)`, review, sentiment, trainflag
    - imdb whole: `path = untar_data(URLs.IMDB)`
- create text databunch:
    - `TextDataBunch`: `data_lm = TextDataBunch.from_csv(path, 'texts.csv')`, where **tokenization & numeralization** where performed, and save the preproceed databunch: `data_lm.save()`
    - datablock API:
    -       `data = (TextList.from_csv(path, 'texts.csv', cols='text').split_from_df(col=2).label_from_df(cols=0).databunch())`
```python
# for imdb whole set
data_lm = (TextList.from_folder(path)
          #Inputs: all the text files in path
          .filter_by_folder(include=['train', 'test', 'unsup'])
          #We may have other temp folders that contain text files so we only keep what's in train and test
          .split_by_rand_pct(0.1)
          #We randomly split and keep 10% (10,000 reviews) for validation
          .label_for_lm()
          #We want to do a language model so we label accordingly
          .databunch(bs=bs))
data_lm.save('data_lm.pkl')
```
- train:
    - language model learner with Wikitext 103 weights: `learn = language_model_learner(data_lm, AWD_LSTM, drop_mult=0.3)`
    - find learning rate: `learn.lr_find()`, `learn.recorder.plot(skip_end=15)`
    - start fine tune:`learn.fit_one_cycle(1, 1e-2, moms=(0.8,0.7))`, `learn.unfreeze()`, `learn.fit_one_cycle(10, 1e-3, moms=(0.8,0.7))`, `learn.save('fine_tuned')`

### Reference
https://builtin.com/data-science/recurrent-neural-networks-powerhouse-language-modeling


## python modules
### pathlib
- `import pathlib`
- path = PosixPath('foo/bar')
- `path.ls()`:
  [PosixPath('/home/data/annotations'),
  PosixPath('/home/data/images')]
- new_path = path/'annotations'
