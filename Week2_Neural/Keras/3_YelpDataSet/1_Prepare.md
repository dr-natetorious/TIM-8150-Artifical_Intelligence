# Process and Classify the Yelp Dataset

## How do I download the images into SageMaker

```bash
# Download the content from S3
aws s3 cp --recursive s3://nbachmei.yelp/images/ ~/SageMaker/Yelp/images/
aws s3 cp s3://nbachmei.yelp/photo/photos.json photos.json

# Create the output folders
mkdir -p labeled labeled/food labeled/menu labeled/inside labeled/outside labeled/drink
mkdir -p grey-scaled grey-scaled/food grey-scaled/menu grey-scaled/inside grey-scaled/outside grey-scaled/drink
```

## How do I sort and normalize them

```python
import jsonlines
import pathlib
import shutil
from PIL import Image

with jsonlines.open('photos.json') as reader:
    for obj in reader:
        photo_id = obj['photo_id']
        label = obj['label']

        # Confirm the file exists
        file = pathlib.Path('images/{id}.jpg'.format(id=photo_id))
        if not file.exists():
            print('missing {file}'.format(file=str(file)))
            continue

        # Copy into the labeled bucket
        output ='labeled/{label}/{id}.jpg'.format(label=label, id=photo_id)
        shutil.copyfile(str(file),output)

        # Grey scale and reduce to 64x64
        im = Image.open(str(file))
        im = im.resize((64,64), Image.ANTIALIAS)
        im = im.convert('L')

        thumbnail ='grey-scaled/{label}/{id}.jpg'.format(label=label, id=photo_id)
        im.save(thumbnail, "JPEG")
