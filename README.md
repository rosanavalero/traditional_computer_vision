# Traditional Computer Vision Techniques - Museum Painting Retrieval 
Project of the Module 1: 'Introduction to Human and Computer Vision' of the Master's degree in Computer Vision at Universitat Autònoma de Barcelona (UAB)

## Summary
This project implements a query-by-example retrieval system for museum images, utilizing conventional computer vision methods. The system retrieves images based on color, texture, text information, keypoints, and local descriptors. Techniques such as denoising, background removal, and orientation correction are applied to enhance image quality. Morphological filters are employed to detect and eliminate overlaid text. The system’s performance is primarily evaluated using the MAP@k metric.

See [Report]()

## Weekly Slides:
- [Week 1](https://docs.google.com/presentation/d/1fK93Q6sRxi8e0b7KvLUawMESzf9BOoVj9ZeOsXoG6y4/edit?usp=sharing)
- [Week 2](https://docs.google.com/presentation/d/11cB84VPgsNNoeIfvGW83xz_N_j840_NGXk48IUHh434/edit?usp=sharing)
- [Week 3](https://docs.google.com/presentation/d/1Wlf__5Gy2G0i28nD2zKjPGsY-QObLRlBKLlWUXic8D8/edit?usp=sharing)
- [Week 4](https://docs.google.com/presentation/d/1ui6RbXL2kv7skn7dz1DNrybpF5IVpJ9XChNonC3I5GI/edit?usp=sharing)
- [Week 5](https://docs.google.com/presentation/d/1alWtXwuB8QduvPyd-_w-MnWFs0u2NOHykGXclJiL3Tk/edit?usp=sharing)


## Contributors
- Julia Ariadna Blanco Arnaus
- Hicham El Muhandiz
- Marcos Muñoz González
- Rosana Valero Martínez

## Activation of the environment
In order to be able to run the scripts below, first it must be activated an environment containing the modules described in the requirements.txt file. To activate the environment, the following command has to be executed:

```
pip install virtualenv

python -m venv .   #inside this repo

source env/Scripts/activate

pip install -r requirements.txt


```

## Usage of the scripts 
### compute_descriptors.py: 
- This script creates a .pkl file containing a list of Image objects given database path. Image objects contain traits to describe each database image such as the image pixel information and the descriptor associated to it (histogram).

  Example of usage:

  Assuming that `inputDir` is the path of the folder containing the database, the following can be executed to compute the descriptors with the default values (generated pickle path: `./database.pkl`, histogramType: `GRAYSCALE` , nbins: `16`)

```
python compute_descriptors.py inputDir 
```

Another example could be: 
```
python compute_descriptors.py inputDir --nbins 16 --histogramType HSV 
```
The available option values can be displayed executing the help command:
```
python compute_descriptors.py --help
```

### compute_similarity.py: 
- This script computes the similarity between a set of query images and the database previously generated with ``compute_descriptors.py`` (database.pkl). In particular, it  obtains the K most similar images to each query as well as computing the MAPK of the entire set compared to the ground truth specified in the query folder. Moreover, if the option `--removeBG` is set to `HSV`, `OTSU` or `LAB`, it will remove the background of each query image and compute the similarity taking into account only the pixels classified as foreground of each query. Likewise, if this option is enabled (!=False), the Fscore measures of the background removal task masks will be outputted as well.

The output files is a .pkl file containing a list of lists with the K most similar images to each query. If the background removal option is enabled, the resulting binary masks will also be outputted in .png format in the directory specified by --saveResultsPath (although left as an option, it is encouraged to set a specific results path so that masks don't get created in the current directory)
  Example of usage:

  Assuming that `inputDir` is the path of the folder containing the queries, the following can be executed to compute the similarity with the default values
```
python compute_similarity.py inputDir 
```

Another example could be: 
```
python compute_similarity.py inputDir --distance X2 --K 10 --saveResultsPath ResultsDir  --GT False --removeBG OTSU
```
The flag GT must be set to False to test it without a ground truth. 
The available option values can be displayed executing the help command:
```
python compute_similarity.py --help
```
