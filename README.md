# Dataset: News Articles in Brazilian Portuguese

This dataset contains 500 news articles in brazilian Portuguese divide into 5 types: 

 - economy
 - entertainment
 - science and technology
 - sports
 - politics

### How to Download and Use Project Dataset

Download as a zip file
```
wget https://github.com/mauricio-seiji/Dataset-news-articles-pt-br/archive/main.zip
```

Unzip files
```
unzip -qq -o main.zip
```

View the downloads folder
```
ls Dataset-news-articles-pt-br-main/
```

### Hot to Use with TensorFlow

After downloading the data set read the files in the unzipped folder and create a validation set using an 80:20 split of the training data.

```
from tensorflow.keras import preprocessing

train_dir = "Dataset-news-articles-pt-br-main/"
batch_size=32
seed = 42

raw_train_ds = preprocessing.text_dataset_from_directory(
    train_dir,
    batch_size=batch_size,
    validation_split=0.2,
    subset='training',
    seed=seed)
```

Getting validation subset.
```
raw_val_ds = preprocessing.text_dataset_from_directory(
    train_dir,
    batch_size=batch_size,
    validation_split=0.2,
    subset='validation',
    seed=seed)
```

Print out a few examples from the training dataset.
```
for text_batch, label_batch in raw_train_ds.take(1):
  for i in range(5):
    print("Text: ", text_batch.numpy()[i][:50], '...')
    print("Label:", label_batch.numpy()[i])
```

The labels in the data set are numbers. You can see the string label for each numbered label.
```
for i, label in enumerate(raw_train_ds.class_names):
  print("Label", i, "corresponds to", label)
```

More details read [Load dataset from text files](https://www.tensorflow.org/tutorials/load_data/text#load_the_dataset)
