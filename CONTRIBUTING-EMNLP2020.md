# How to Contribute to EMNLP-2020

Notes: see [CONTRIBUTING.md](./CONTRIBUTING.md) for general instructions.

## Setup Environment

Before you start, please make sure you have a GitHub account and have your ssh key added to your GitHub account. Also, 
Python should be installed into your device to setup the environment.

### Get the GitHub Repository
You can either do it with git in the command line, or via the website.

#### Option 1. Via command line and git
```shell
cd /path/to/the/local/folder
git clone git@github.com:emnlp-org/emnlp-2020-virtual-conference.git
```

#### Option 2. Direct download
If you are not familiar with ```git```, you can download the content by clicking the green button and the "Download ZIP"
 button and extract to your local folder.

### Install Required Software Dependencies

#### Optional: Create a Virtual Environment
Creating a virtual Python environment makes sure that all the Python libraries installed in it do not conflict with the 
software already on your machine. It is not mandatory, but will prevent a number of bugs.

There are many ways to create virtual environments in Python, use your favorite venv manager, or use the following 
commands to create one using ```virtualenvwrapper``` with Python **3.x (x=7 or above)**.

1) Install python and virtualenvwrapper
```shell
#----------------------------------------------------
# on Ubuntu
sudo apt-get install python3-pip
sudo pip3 install virtualenvwrapper
#----------------------------------------------------
# on MacOS
# install if needed
brew install python3
```

2) Find the path to what you just installed
```shell
which python3 # find the path to python3.x
which virtualenvwrapper.sh # find the path to the virtualenverapper installation script
# Open the bashrc file
nano ~/.bashrc
```
3) Change the bash script file to activate wrapper. 
Modify the following lines accordingly and add them at the end of the ~/.bashrc file, which you just opened with nano
```shell
export VIRTUALENVWRAPPER_PYTHON='the output of which python3'
source 'the output of which virtualenvwrapper.sh'
```
When you are done, close ~./bashrc by pressing ctrl+x and save the changes by pressing "y".
4) Refresh the bash profile
```shell
source ~/.bashrc
```
5) Create a virtual environment for emnlp
```shell
mkvirtualenv --python='the output of which python3' your_env_name
```
You now have a python3.x virtual environment specificaly for emnlp-2020. If you accidentally quit this environment, you 
can reactivate the environemnt by the following code `workon your_env_name`

#### Install the packages
In the emnlp-2020-virtual-conference folder.

```shell
# Move to the repository folder
cd emnlp-2020-virtual-conference
# install required packages
pip install -r requirements.txt
```

## How to Create a Pull Request for the Website

As mentioned in the [GitHub help documentation](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request),
creating a pull request can propose and collaborate on changes to a repository. Those changes will be proposed to a *branch*, 
which ensures that the ```master``` branch only contains finished and approved works. 


### Change Code on a Branch 
#### Create a Branch
```shell
# pull the newest update from the master branch
git pull
# create local branch
git checkout -b your_branch_name
```

#### Save your Changes
By now you have created a new local branch. Then you can make contributions to the content. 
You can save your contributions on your local git by commiting.
```shell
git add . # add all files
git add file_changed # only add file the named file_changed
git commit -am 'what i did in this commit'
```

#### Run Code Checks
When you think you are good, you should check that you code passes the github checks
```shell
# Auto formats your code
make format
# Run all checks locally
make
```
If the second command fails, you need to fix the errors it indicates (and commit your fixes). (A warning is not a problem, 
however an error must be fixed)

#### Push your modifications
Once you've finished, use the following command in the terminal to push your changes to the global repository, on your branch.

```shell
git push --set-upstream origin your_branch_name # setup the upstream
```

### Opening a Pull Request in the Main Repository

Now you can open a pull request on the repository's website. Additionally, on the repository's page, you should click 
```New pull request``` button near the ```Branch: master```. Then it will redirect to a new page. On this page, you 
need to be very carefully for the choices of base repository and head repository. Following the example shown in this 
document, the head repository should be ```emnlp-org/emnlp-2020-virtual-conference```, and ```compare: your_branch_name``` 
next to the head repository menu. The base repository should be ```emnlp-org/emnlp-2020-virtual-conference```.  Then you
 can click the green button ```Create pull request```. By clicking this button, you have created a new pull request and a 
 collaborator will be notified and review your changes. The collaborator will discuss any further changes for your 
 contributions. Once approved, your branch will be merged into ```master``` branch. Before you make any further contributions, 
 don't forget to ```git pull``` to update your local files.

For more details about opening a pull request on the website, please check the  
[GitHub help documentation](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request).

## Code overview
The general code logic and structure is detailed in the 
[README](https://github.com/emnlp-org/emnlp-2020-virtual-conference/blob/master/README.md), it will help you follow what 
folder does what if you are not familiar with webdev.

## Where is What: Example of the Sponsors/Virtual Booths

### Logic
Each sponsor has a virtual booth where they can give an introduction about
themselves, share resources like links or files, show a video and inform
about live recruiting events taking place during the conference. Two pages 
are relevant for that, `sponsors.html` (overview of all sponsors) and
`sponsor.html` (the virtual booth for each sponsor).

### Data
The data used to generate these pages is sourced from `sponsors.yml`. Grouped
by sponsor level, there is an entry for every sponsor containing information
like name, logo, a link to their website, event schedule and more.

Please refer to the [format description](doc/dataformats.md)
for which fields exist and which are optional.

#### Managing Duplicates

In case a sponsor is listed in two levels, the entries after the first mention
of this sponsor  should only contain `UID`, `name` and `duplicate: yes`. This
is e.g. the case for DeepMind and Grammarly.
 
### Page Templates 

There are two templates that are important for the sponsors, `sponsors.html` (overview of all
sponsors) and `sponsor.html` (the virtual booth for each sponsor).

##### Individual page (`sponsor.html`)

The page is divided into three parts: the introduction of the sponsor, video and
then the different sections. Sections use [Bootstrap Accordions](https://getbootstrap.com/docs/4.3/components/collapse/#accordion-example). 
If you want to add a new section, copy one of the existing and make sure to add a guard
checking whether the related variables are defined if it is optional. 

## FAQ

Q: Where should I put images for EMNLP2020?
A: All images should be saved under [static/images/emnlp2020](https://github.com/emnlp-org/emnlp-2020-virtual-conference/pull/114/files/static/images/emnlp2020) folder.


Q: How can I update the website with my changes?
A: The GitHub action will automatically updates virtual.2020.emnlp.org once your PR is merged.

Q: My branch has failed cheks, what should I do?
A: Please run `make format` and `make`, fix the errors, and commit again to your branch.
