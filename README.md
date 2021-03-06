# Right Whale Identification

<h2>Introduction</h2>

This is the repository for team DAND's (I am open to any alternate suggestions for a name - Fine and DANDy?, DANDy Lions?) entry in the Kaggle Competiton [Right Whale Recognition](https://www.kaggle.com/c/noaa-right-whale-recognition). The team is composed of graduates of Udacity's Data Analyst Nanodegree. The purpose of this competition is to build an algorithm that can identify specific whales from overhead photographs. See the [resources.md](resources.md) file above for a (growing) list of resources for this project.

The problem consists of two separate tasks - whale recognition (finding a whale in a larger picture) and whale identification (identifying a specific whale based on its picure). We may also wish to explore the possibility that it is not necessary to perform whale recognition.<br>

<h2>Data</h2>

Data files provided by Kaggle are located in the [Data](Data) folder above. Each row of the data links an `Image` with a `whaleID`. There are 11468 images of whales in the `imgs` folder. The `imgs` folder is not on the git because it is over 9GB. Get the images [here](https://www.kaggle.com/c/noaa-right-whale-recognition/data) and put the unzipped `imgs` folder one level above your local clone so that any code we write will be able to find them there. There are labelled data for 4543 of those images and the remaining 6925 are unlabelled. For each unlabeled image our model should output a vector of predicted probabilities, one for each of the 447 whales in the dataset. For more on how entries are evaluated see [this description](https://www.kaggle.com/c/noaa-right-whale-recognition/details/evaluation).

Within the training set there are some whales with very many associated images (as many as 47) and many whales with only a few images (or even just 1 in some cases). The file [ExploreData.ipynb](ExploreData.ipynb) above can help with exploring the data and viewing the images. It is a good idea to spend some time checking out the pictures to get a feel of what we are working with. The characteristics of the images in question are likely to dictate decisions about how to proceed.

<h2>Methodology</h2>

As noted, there are two separate tasks we must perform - recognition and identification. We should retain modularity with respect to these tasks so that they can be developed separately, perhaps by different teams. 

~~The competition site provides a short tutorial on using MatLab to build a whale recognizer and all participants in the contest are entitled to a free MatLab license (let me know if you need one) so I think that we should use MatLab to build our whale recognizer.~~
<br>
Actually, the more I think about this, the more I think we should try to build our recognizer with [OpenCV](http://docs.opencv.org/master/index.html#gsc.tab=0). I have written a description of how I was able to train a recognizer (aka classifier) which you can find [here](Using%20AWS%20to%20Train%20a%20Cascade%20Classifier.md)

Since they have been used succesfully by past Kaggle winners in [predicting how galaxy images will be classified](http://benanne.github.io/2014/04/05/galaxy-zoo.html), [identifying types of plankton](http://benanne.github.io/2015/03/17/plankton.html), and [identifying stages of eye disease](http://blog.kaggle.com/2015/08/10/detecting-diabetic-retinopathy-in-eye-images/), I recommend that we try to (eventually) implement a Convolutional Neural Network(CNN) for the whale identification stage. No doubt this is easier said than done.

I am also open to any other suggestions as to how we might approach the task.<br/>

<h2>Right Whales</h2> 

Check out this [website](http://www.neaq.org/conservation_and_research/projects/endangered_species_habitats/right_whale_research/right_whale_projects/monitoring_individuals_and_family_trees/identifying_with_photographs/how_it_works/callosity_patterns.php) which gives information about how scientists identify individual right whales. It is primarily based on the pattern of white callosity on the nose of the whale, but be sure to click the link at the bottom for other features used. Check out the [resources.md](resources.md) file for more links to information about whale identification.

<h2>Now . . .</h2>

If you are interested in participating you should:
 - thoroughly read over all the information on the [competion site](https://www.kaggle.com/c/noaa-right-whale-recognition) and browse the [forum](https://www.kaggle.com/c/noaa-right-whale-recognition/forums) as well.
 - orient yourself to the task by learning a little about right whale identification
 - read the three Kaggle winners blogs linked above (or any others from [here](http://blog.kaggle.com/category/dojo/))
 - check out the image files of the whales to see what we are working with
 - let me know (kburnham@gmail.com) so that I can add you to the team on Kaggle and we can start planning how to proceed
 - we need to find out a good way for us all to communicate which github does not seem to provide. It may be possible to do this through Kaggle, but I am not certain. Any ideas?


 <h2>Moving Forward</h2>

There are three main tasks before us to accomplish our goal, described below. All of this is, of course, subject to change based on future developments. If anyone has a better idea for how to approach these problems, please do speak up. I think we should start by trying to build a functional model on a small subset of data (20 pictures of 2 whales) and then trying to scale up from there. Image files and a dataset for this are in the [data_subset](data_subset).

1. Obtain a set of training images for our whale recognizer. This is a fairly tedious task and involves cropping whale images out of the full image files for use by the `opencv_createsamples` utility. We also need negative images (those that do not contain whales) and background images to feed into the utility. We need to decide exactly how the cropping should be done (e.g. the entire visiable whale, or just the forehead?) and spend time experimenting with OpenCV to see how the image recognizer works. The whale images cropped at this stage can also be used to train the identifier in part 3. One of the other participants has designed a python program to help with this process. See [this post](https://www.kaggle.com/c/noaa-right-whale-recognition/forums/t/16275/python-script-to-sort-images/91584#post91584).

2. Train a whale recognizer takes in photo and returns that subsection of the photo that contains a whales. This image will then be passed to the identifier in part 3. As noted above there is a tutorial on Kaggle that uses MatLab for this process, but I have not had much luck with it and would prefer that we instead try to use OpenCV for this purpose. I would rather get practice using Python than try to learn something new (for me at least). It also means that the skills we acquire will be more generalizable. Check out the [documentation on OpenCV's Cascade Classifier Trainer](http://docs.opencv.org/doc/user_guide/ug_traincascade.html#viola2001). You can find tutorials for OpenCV-Python [here](https://opencv-python-tutroals.readthedocs.org/en/latest/py_tutorials/py_tutorials.html).

3. Train an identifier that, given a cropped image of a whale, identifies that whale. In fact the identifier should output a vector of probabilities, one for each whale in the dataset. As noted above, I believe that the best way to do this is through the use of a Convolutional Neural Network which has been succesfully used for many other image related tasks. However, before we do that I think we should try to implement a very simple model to get started and then brainstorm as to how we want to move forward from there.








