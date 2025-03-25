# CenterTrack_setup
This is an instructional guide to set up CenterTrack repository on windows

Setup:

1. Install and run WSL (I did this through the VSCODE installation of WSL) Ubuntu version 24.04

2. Install latest version of anaconda following this tutorial: https://gist.github.com/kauffmanes/5e74916617f9993bc3479f401dfec7da

3. Create CenterTrack anaconda environment using python 3.6.13 (conda create --name CenterTrack python=3.6)

4. Activate CenterTrack environment (conda activate CenterTrack)

5. Install PyTorch GPU enabled using: (pip install torch==1.4.0+cu100 -f https://nelsonliu.me/files/pytorch/whl/torch_stable.html) this was taken from repository https://github.com/nelson-liu/pytorch-manylinux-binaries?tab=readme-ov-file

6. Run (pip install torchvision==0.5.0) 

7. Follow the install.md file for CenterTrack starting at step 2 wait before performing step 4 (we already performed step 1) https://github.com/xingyizhou/CenterTrack/blob/master/readme/INSTALL.md

8. If opencv is giving you problems use (pip install opencv-python==4.5.4.60)

Note: I was having issues with xcb and ran this which seemed to fix the issue: (
    sudo apt update
    sudo apt install -y libxcb-xinerama0 libxcb-xinerama0-dev \
    libxkbcommon-x11-0 libxcb1 libxcb-util1 libxcb-icccm4 libxcb-image0 \
    libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 libxcb-shape0 \
    libxcb-xfixes0 libxcb-sync1 libxcb-xinerama0)


9. Before you continue in the install.md file, you need to install cudatoolbox installer. Installer: https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=deb_local

10. Install the cudatoolbox: (sudo apt install nvidia-cuda-toolkit)

11. Run:
(export CUDA_HOME=/usr/local/cuda
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH
export CXXFLAGS="${CXXFLAGS} -D__CUDA_NO_HALF_OPERATORS__ -D__CUDA_NO_HALF_CONVERSIONS__ -D__CUDA_NO_HALF2_OPERATORS__")

12. Clone the DCNv2 repo that is listed in install.md

13. When in the DCNv2 repo run (python setup.py build develop) I also needed to run (./make.sh)

14. Test to make sure that you are connected via gpu by running the testcuda.py script in the DCNv2 directory (python testcuda.py)

15. Attempt to run the demo.py file in the CenterTrack/src directory using (python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633)

16. If you are getting an error related to the tuples having an invalid type go to the directory /root/CenterTrack/src/lib/utils/debugger.py and open the file to edit. Changing 
lines I changed lines 379-381 to: 
cv2.line(bird_view, (int(rect[e[0]][0]), int(rect[e[0]][1])), (int(rect[e[1]][0]), int(rect[e[1]][1])),
    lc, int(t),
    lineType=cv2.LINE_AA
)

Other things that I ran and am unsure if made a difference:

sudo apt install -y libxcb-xinerama0 libxcb-xinerama0-dev     libxkbcommon-x11-0 libxcb1 libxcb-util1 libxcb-icccm4 libxcb-image0     libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 libxcb-shape0     libxcb-xfixes0 libxcb-sync1 libxcb-xinerama0

sudo apt install -y libgtk2.0-dev pkg-config







History of commands that I ran in case I missed anything. Many of these commands did not function or were not needed, but may be important to note: 


      103  git clone https://github.com/xingyizhou/CenterTrack.git
      104  cd CenterTrack/
      105  conda info
      106  bash Anaconda3-2024.10-1-Linux-x86_64.sh
      107  mv Anaconda3-2024.10-1-Linux-x86_64.sh ~
      108  cd ~
      109  ls
      110  bash Anaconda3-2024.10-1-Linux-x86_64.sh
      111  pwd
      112  cd /
      113  pwd
      114  cd root/
      115  ls
      116  bash Anaconda3-2024.10-1-Linux-x86_64.sh
      117  which python
      118  which python3
      119  conda info
      120  cd CenterTrack/
      121  conda create --name CenterTrack python=3.6
      122  conda activate CenterTrack
      123  conda install pytorch=1.0.0 torchvision cudatoolkit=10.0 -c pytorch
      124  pip install torch==1.4.0+cu100 -f https://nelsonliu.me/files/pytorch/whl/torch_stable.html
      125  pip install cython; pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
      126  pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
      127  pip install numpy
      128  pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
      129  sudo apt-get update && sudo apt-get upgrade -y
      130  sudo apt autoremove -y
      131  sudo apt-get install gcc -y
      132  gcc --version
      133  pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
      134  cd src/lib/model/networks/
      135  cd ~
      136  rm -r CenterTrack/
      137  git clone --recursive https://github.com/xingyizhou/CenterTrack $CenterTrack_ROOT
      138  cd CenterTrack/
      139  pip install -r requirements.txt
      140  sudo apt update
      141  sudo apt install ninja-build cmake build-essential
      142  pip install -r requirements.txt
      143  pip install opencv-python==4.5.4.60
      144  pip install -r requirements.txt
      145  cd src/lib/model/networks/
      146  git clone https://github.com/CharlesShang/DCNv2/
      147  cd DCNv2/
      148  ./make.sh
      149  cd ~/CenterTrack/
      150  mkdir models
      151  cd models/
      152  cd /
      153  cd mnt
      154  cd c
      155  ls
      156  cd Users/
      157  ls
      158  cd IPCLAB/
      159  ls
      160  cd 3d_attempts/
      161  ls
      162  cd centerT/CenterTrack/
      163  ls
      164  cd models/
      165  ls
      166  cp nuScenes_3Dtracking.pth ~/CenterTrack/models/
      167  cd ~
      168  cd CenterTrack/models/
      169  ls
      170  cd ..
      171  cd src/
      172  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      173  pip install torchvision==0.5.0
      174  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      175  sudo apt update
      176  sudo apt install -y libxcb-xinerama0 libxcb-xinerama0-dev     libxkbcommon-x11-0 libxcb1 libxcb-util1 libxcb-icccm4 libxcb-image0     libxcb-keysyms1 libxcb-randr0 libxcb-render-util0 libxcb-shape0     libxcb-xfixes0 libxcb-sync1 libxcb-xinerama0
      177  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      178  conda activate CenterTrack
      179  cd CenterTrack/
      180  pip uninstall opencv-python
      181  pip install opencv-python-headless==4.5.4.60
      182  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      183  cd src/
      184  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      185  pip install install libgtk2.0-dev
      186  sudo apt update
      187  sudo apt install -y libgtk2.0-dev pkg-config
      188  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      189  lspci | grep -i nvidia
      190  apt install pciutils
      191  lspci | grep -i nvidia
      192  cd /
      193  lspci | grep -i nvidia
      194  cd CenterTrack/
      195  ls
      196  cd src
      197  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      198  conda activate CenterTrack
      199  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      200  pip uninstall opencv-python opencv-python-headless
      201  pip install opencv-python==4.5.4.60
      202  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      203  cd lib/model/networks/DCNv2/
      204  python testcuda.py
      205  cd ..
      206  rm -r DCNv2/
      207  git clone https://github.com/CharlesShang/DCNv2.git
      208  cd DCNv2/
      209  import torch
      210  print(torch.cuda.is_available())  # Should return True
      211  print(torch.__version__)          # Should match your installed CUDA version
      212  python
      213  python setup.py build develop
      214  python testcuda.py 
      215  ./make.sh 
      216  python testcuda.py 
      217  python test
      218  python test.py 
      219  cd ~
      220  cd CenterTrack/
      221  cd src/
      222  ls
      223  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      224  nvcc –V 
      225  wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
      226  sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
      227  wget https://developer.download.nvidia.com/compute/cuda/12.8.1/local_installers/cuda-repo-ubuntu2004-12-8-local_12.8.1-570.124.06-1_amd64.deb
      228  sudo dpkg -i cuda-repo-ubuntu2004-12-8-local_12.8.1-570.124.06-1_amd64.deb
      229  sudo cp /var/cuda-repo-ubuntu2004-12-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
      230  sudo apt-get update
      231  sudo apt-get -y install cuda-toolkit-12-8
      232  sudo apt-get install -y cuda-drivers
      233  sudo apt-get install -y nvidia-open
      234  lsb_release -a
      235  sudo apt install nvidia-cuda-toolkit
      236  nvcc –V 
      237  ncvv -v
      238  nvcc -v
      239  cd lib/model/networks/
      240  cd DCNv2/
      241  python testc
      242  python testcuda.py 
      243  ~/CenterTrack/src/lib/model/networks/DCNv2
      244  cd ~/CenterTrack/src/lib/model/networks/DCNv2
      245  conda activate CenterTrack
      246  python testcuda.py 
      247  cd ..
      248  rm -r DCNv2/
      249  sudo apt install nvidia-cuda-toolkit
      250  git clone https://github.com/CharlesShang/DCNv2.git
      251  export CUDA_HOME=/usr/local/cuda-11 
      252  cd DCNv2/
      253  ./make.sh 
      254  python testc
      255  python testcuda.py 
      256  python setup.py build develop
      257  python testcuda.py 
      258  rm -r build/
      259  export CUDA_HOME=/usr/local/cuda
      260  export PATH=$CUDA_HOME/bin:$PATH
      261  export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH
      262  python setup.py build develop
      263  python testcuda.py 
      264  cd ~/CenterTrack/src/
      265  ls
      266  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
      267  cd lib/
      268  cd model/
      269  cd networks/
      270  cd DCNv2/
      271  rm -rf build _ext.cpython-36m-x86_64-linux-gnu.so
      272  export CXXFLAGS="${CXXFLAGS} -D__CUDA_NO_HALF_OPERATORS__ -D__CUDA_NO_HALF_CONVERSIONS__ -D__CUDA_NO_HALF2_OPERATORS__"
      273  python setup.py build develop
      274  python testcuda.py 
      275  cd ~/CenterTrack/src/
      276  python demo.py tracking,ddd --load_model ../models/nuScenes_3Dtracking.pth --dataset nuscenes --pre_hm --track_thresh 0.1 --demo ../videos/nuscenes_mini.mp4 --test_focal_length 633
