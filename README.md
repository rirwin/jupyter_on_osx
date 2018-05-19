# jupyter_on_osx

/usr/bin/python is python 2.7.10

From https://brew.sh/
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# enter your password

# Installs xcode if you haven't already


brew install python@2

# installs pip at /usr/local/bin/pip
# /usr/local/bin/python2.7  python 2.7.15


pip install virtualenv

# installs virtualenv at /usr/local/bin/virtualenv

# clone the repo
git clone https://github.com/rirwin/jupyter_on_osx.git

virtualenv virtualenv_run
source virtualenv_run/bin/activate
pip install -r requirements.txt
jupyter notebook

if your browser doesn't open a new tab, 
hold command key and click on link (look like http://localhost:8888/?token=5490a2c744f...)

Make sure the above works then hit ctrl-c to cancel, hit y to shutdown server

# get dataset
https://www.kaggle.com/yelp-dataset/yelp-dataset/downloads/yelp-dataset.zip/6
https://www.kaggle.com/yelp-dataset/yelp-dataset/version/6#_=_
https://www.kaggle.com/yelp-dataset/yelp-dataset/kernels


mkdir data/
mv ~/Downloads/yelp-dataset.zip ./data
cd data/
unzip yelp-dataset.zip
cd ../

jupyter notebook

# Click 'New' and then Folder.  
# Check the box next to the new folder probably named 'Untitled' and rename to 'notebooks'
# Click on the 'notebooks' folder
# Click 'New' and then 'Python 2'

# This starts your first notebook!

# Click 'Untitled' to name it.

# Paste the following in the first cell and hold shift and hit enter
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

import seaborn as sns
%matplotlib inline

# In the second cell paste the following and shift-enter again (takes 1-2 minutes):
business=pd.read_csv("../data/yelp_business.csv")
business_attributes=pd.read_csv("../data/yelp_business_attributes.csv")
business_hours=pd.read_csv("../data/yelp_business_hours.csv")
check_in=pd.read_csv("../data/yelp_checkin.csv")
reviews=pd.read_csv("../data/yelp_review.csv")
tip=pd.read_csv("../data/yelp_tip.csv")
user=pd.read_csv("../data/yelp_user.csv")

# The above loads data into what's called pandas data frames: In the third cell
business.head()

# In the fourth cell we can plot the review rating distribution by running the following

# https://www.kaggle.com/jagangupta/what-s-in-a-review-yelp-ratings-eda

# Get the distribution of the ratings
x = business['stars'].value_counts()
x = x.sort_index()

# plot
plt.figure(figsize=(8,4))
ax = sns.barplot(x.index, x.values, alpha=0.8)
plt.title("Star Rating Distribution")
plt.ylabel('# of businesses', fontsize=12)
plt.xlabel('Star Ratings ', fontsize=12)

# adding the text labels
rects = ax.patches
labels = x.values
for rect, label in zip(rects, labels):
    height = rect.get_height()
    ax.text(rect.get_x() + rect.get_width()/2, height + 5, label, ha='center', va='bottom')

plt.show()


