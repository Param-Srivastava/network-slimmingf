<div align="center">
  <h1>📖 Network Slimming</h1>
  <p>Optimizing deep Convolutional Neural Network</p>
</div>
<p align="center">
</p>

Source code folder [link](https://drive.google.com/drive/folders/1lrY4gBAcqBVyPP3ps7TneOn5UnO9Rnv5?usp=sharing)

Dataset [link](https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz)   163 MB

## Transfer Files to Server

Using the command below, I transfered the file from my local machine to the [ParamShivay](https://nsmindia.in/node/155) server.

```bash
scp -P 4422 -r "C:/Users/Param Srivastava/OneDrive/Desktop/network-slimmingf/" paramsri.civ21.itbhu@172.16.40.30:/scratch/paramsri.civ21.itbhu/
```

## Connect to Server via SSH

After entering the below command, the server prompts for a Captcha followed by the user's Password.

```
ssh  paramsri.civ21.itbhu@paramshivay.iitbhu.ac.in
```

## Set Up Conda Environment

After loading the conda module, we activate the source, then we create our own virtual environment `mypytorch`. Then we installed pytorch and required dependencies by running following `conda install` util.

```
ml load conda/4.8.3
source activate
conda create --name mypytorch python=3.9
conda activate mypytorch
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

## Create and Submit Job Script

Given below is a template for submitting the Job Script by following mentioned steps.

```
vim script.sh
# Press 'i' to enter text, paste the following:

#!/bin/bash
#SBATCH --job-name=param_netslim
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=40
#SBATCH --time=96:00:00
#SBATCH --partition=gpu
#SBATCH --gres=gpu:2
#SBATCH --output=%J.out
#SBATCH --error=%J.err

source activate
conda activate pytorch

cd /scratch/paramsri.civ21.itbhu/network-slimmingf

python3 main.py

# Press 'Shift+esc' and type ':wq' to save and exit
```

## Submit the Job

Below single line submits the job and starts execution.

```
sbatch script.sh
```

## View Job Output

My job ID was 919787, and correspondingly I used the following commands to view my output file `919787.out`.

```
# To see the static output file
cat 919787.out

# To see the dynamic output file
tail -f 919787.out
```
