# FUNCTIONS

The first rule of functions is that they should be small. The second rule of functions is that
they should be smaller than that. 

You want your Python function to:

* be small
* do one thing
* contain code with the same level of abstraction
* have fewer than 4 arguments
* have no duplication
* use descriptive names

```python
def main():

    load_data(
        url="https://drive.google.com/uc?id=1jI1cmxqnwsmC-vbl8dNY6b4aNBtBbKy3",
        output="Twitter.zip",
        path_train="Data/train/en",
        path_test="Data/test/en",
    )


def load_data(url: str, output: str, path_train: str, path_test: str):

    # Download data from Google Drive
    output = "Twitter.zip"
    gdown.download(url, output, quiet=False)

    # Unzip data
    with zipfile.ZipFile(output, "r") as zip_ref:
        zip_ref.extractall(".")

    # Get train, test data files
    tweets_train_files = [
        file
        for file in listdir(path_train)
        if isfile(join(path_train, file)) and file != "truth.txt"
    ]
    tweets_test_files = [
        file
        for file in listdir(path_test)
        if isfile(join(path_test, file)) and file != "truth.txt"
    ]

    # Extract texts from each file
    t_train = []
    for file in tweets_train_files:
        train_doc_1 = [r.text for r in ET.parse(join(path_train, file)).getroot()[0]]
        t_train.append(" ".join(t for t in train_doc_1))

    t_test = []
    for file in tweets_test_files:
        test_doc_1 = [r.text for r in ET.parse(join(path_test, file)).getroot()[0]]
        t_test.append(" ".join(t for t in test_doc_1))

    return t_train, t_test


if __name__ == "__main__":
    main()

```

Function, it is difficult to understand what this function does in 3 minutes. It is because:

* The function is awfully long
* The function tries to do multiple things
* The code within the function is at multiple levels of abstractions.
* The function has more than 3 arguments
* There are multiple duplications
* Function’s name is not descriptive

## small
```python
import zipfile

def unzip_data(output: str):
  
    with zipfile.ZipFile(output, 'r') as zip_ref:
        zip_ref.extractall('.')
```

## Do One Task

```python
download_zip_data_from_google_drive(url, output_path)

unzip_data(output_path)

tweet_train, tweet_test = get_train_test_docs(path_train, path_test)
```

## Duplication

```python
t_train = []
for file in tweets_train_files:
    train_doc_1 =[r.text for r in ET.parse(join(path_train, file)).getroot()[0]]
    t_train.append(' '.join(t for t in train_doc_1))


t_test = []
for file in tweets_test_files:
    test_doc_1 =[r.text for r in ET.parse(join(path_test, file)).getroot()[0]]
    t_test.append(' '.join(t for t in test_doc_1))
```

```python
from typing import Tuple, List

def get_train_test_docs(path_train: str, path_test: str) -> Tuple[list, list]:
    tweets_train_files = get_files(path_train)
    tweets_test_files = get_files(path_test)

    t_train = extract_texts_from_multiple_files(path_train, tweets_train_files)
    t_test  = extract_texts_from_multiple_files(path_test, tweets_test_files)
    return t_train, t_test
    
def extract_texts_from_multiple_files(path_to_file: str, files: list) -> List[str]:

    all_docs = []
    for file in files:
        text_in_one_file = extract_texts_from_each_file(path_to_file, file)
        all_docs.append(text_in_one_file)

    return all_docs
```

## Descriptive Names

function extract_texts_from_multiple_files does by looking at its name.
Don’t be afraid to write long names. It is better to write long names rather than write vague names.

descriptive name of a function is too long such as download_file_from_Google_drive_and_extract_text_from_that_file.
It is a good sign that your function is doing multiple things and you should split it into smaller functions.

## If a function has more than 3 arguments, consider turning it into a class.

Since the functions download_zip_data_from_google_drive , unzip_data , and get_train_test_docs are </br>
all trying to achieve one goal: get data, we could put them into one class called DataGetter .


```python
import xml.etree.ElementTree as ET
import zipfile
from os import listdir
from os.path import isfile, join
from typing import List, Tuple

import gdown


def main():

    url = "https://drive.google.com/uc?id=1jI1cmxqnwsmC-vbl8dNY6b4aNBtBbKy3"
    output_path = "Twitter.zip"
    path_train = "Data/train/en"
    path_test = "Data/test/en"

    data_getter = DataGetter(url, output_path, path_train, path_test)

    tweet_train, tweet_test = data_getter.get_train_test_docs()


class DataGetter:
    def __init__(self, url: str, output_path: str, path_train: str, path_test: str):
        self.url = url
        self.output_path = output_path
        self.path_train = path_train
        self.path_test = path_test
        self.download_zip_data_from_google_drive()
        self.unzip_data()

    def download_zip_data_from_google_drive(self):

        gdown.download(self.url, self.output_path, quiet=False)

    def unzip_data(self):

        with zipfile.ZipFile(self.output_path, "r") as zip_ref:
            zip_ref.extractall(".")

    def get_train_test_docs(self) -> Tuple[list, list]:

        tweets_train_files = self.get_files(self.path_train)
        tweets_test_files = self.get_files(self.path_test)

        t_train = self.extract_texts_from_multiple_files(
            self.path_train, tweets_train_files
        )
        t_test = self.extract_texts_from_multiple_files(
            self.path_test, tweets_test_files
        )
        return t_train, t_test

    @staticmethod
    def get_files(path: str) -> List[str]:

        return [
            file
            for file in listdir(path)
            if isfile(join(path, file)) and file != "truth.txt"
        ]

    def extract_texts_from_multiple_files(
        self, path_to_file: str, files: list
    ) -> List[str]:

        all_docs = []
        for file in files:
            text_in_one_file = self.extract_texts_from_each_file(path_to_file, file)
            all_docs.append(text_in_one_file)

        return all_docs

    @staticmethod
    def extract_texts_from_each_file(path_to_file: str, file_name: list) -> str:

        list_of_text_in_one_file = [
            r.text for r in ET.parse(join(path_to_file, file_name)).getroot()[0]
        ]
        text_in_one_file_as_string = " ".join(t for t in list_of_text_in_one_file)

        return text_in_one_file_as_string


if __name__ == "__main__":
    main()

```

## Blocks and Indenting
The blocks within if statements, else statements, while statements, and
so on should be one line long. Probably that line should be a function call. Not only does
this keep the enclosing function small, but it also adds documentary value because the
function called within the block can have a nicely descriptive name.

```python
if istestpage(pageData):
    includeSetupAndTeardownPages(pageData, isSuite) 
```

# FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.

