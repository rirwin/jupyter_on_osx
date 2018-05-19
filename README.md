# Install brew
Open the terminal app (hit cmd-space, type terminal, enter)

Install Brew, from https://brew.sh/ enter the following command to get brew and enter your user password to install it.
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Use brew to installs python2 if you don't have it already.  This also installs xcode if you haven't already.
```
brew install python@2
```

The import thing is that this installs python2 and pip (at /usr/local/bin/python2.7 and /usr/local/bin/pip respectively)

# Create virtualenv and install jupyter

Next, create a virtualenv, which is an environment for install python libraries that can be isolated from other parts of your operating system.

```
pip install virtualenv
```

This installs virtualenv (at /usr/local/bin/virtualenv).  Then, you are ready to clone the repo.
```
git clone https://github.com/rirwin/jupyter_on_osx.git
```

Go into the directory and start jupyter
```
cd jupyter_on_osx
virtualenv virtualenv_run
source virtualenv_run/bin/activate
pip install -r requirements.txt
jupyter notebook
```

If your browser doesn't open a new tab, hold command key and click on link in the terminal (it looks like http://localhost:8888/?token=5490a2c744f...).

Make sure the above works then hit `ctrl-c` to close, type 'y' to shutdown server

# Get dataset from kaggle
The first link takes you right to the yelp dataset.  You'll need to create an account with kaggle.

https://www.kaggle.com/yelp-dataset/yelp-dataset/downloads/yelp-dataset.zip/6

This takes you to the competion:

https://www.kaggle.com/yelp-dataset/yelp-dataset/version/6#_=_

This takes you to some really helpful kernels that others have created.  Maybe this one will be there too time permitting.

https://www.kaggle.com/yelp-dataset/yelp-dataset/kernels

After you get the dataset execute the following commands (it is presumed the the dataset zip file is in your 'Downloads' folder
```
mkdir data/
mv ~/Downloads/yelp-dataset.zip ./data
cd data/
unzip yelp-dataset.zip
cd ../
```

# Create your first notebook
Back in the terminal start the jupyter server again.
```
jupyter notebook
```

In the browser:
- Click 'New' and then Folder. 
- Check the box next to the new folder probably named 'Untitled' and rename to 'notebooks'.
- Click on the 'notebooks' folder.
- Click 'New' and then 'Python 2'.

This starts your first notebook! Click 'Untitled' to rename it.  Paste the following in the first cell and hold shift and hit enter

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

import seaborn as sns
%matplotlib inline
```

In the second cell paste the following and shift-enter again (takes 1-2 minutes):
```
business=pd.read_csv("../data/yelp_business.csv")
business_attributes=pd.read_csv("../data/yelp_business_attributes.csv")
business_hours=pd.read_csv("../data/yelp_business_hours.csv")
check_in=pd.read_csv("../data/yelp_checkin.csv")
reviews=pd.read_csv("../data/yelp_review.csv")
tip=pd.read_csv("../data/yelp_tip.csv")
user=pd.read_csv("../data/yelp_user.csv")
```

The above loads data into what's called pandas dataframes.  To inspect the dataframe, in the third cell look at the business dataframe.
```
business.head()
```

In the fourth cell we can plot the review rating distribution by running the following.  The credit goes to this helpful kernel: https://www.kaggle.com/jagangupta/what-s-in-a-review-yelp-ratings-eda

```
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
```
