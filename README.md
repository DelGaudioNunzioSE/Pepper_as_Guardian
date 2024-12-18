# Pepper as a Social Robot 🗣️

## Documentation
- https://miro.com/welcomeonboard/UGMxOGxGc2tTM2pNTGxyR0pwM2lvbWdUK09rOVVuWDV1RHJzdXgvOW1LUVl0U3IwQ2RJTHN4U2k3eVc0T3F1UCtWM2xzdFdKTVRFc0NuQWt1TDZKbjI5Sk1nQkVxWktORUxORlIydW44aUtYNTkyeVczcFZ0ZzVIbDJDaWdRM0chZQ==?share_link_id=50079255558

## About this Repository

Welcome to the repository for our **Cognitive Robotics** project! The goal of this project is to develop a **social robot** using **Pepper**, controlled via **ROS** (Robot Operating System).

Pepper will be designed to:
- Interact with humans in a natural way 🧑🤝🤖
- Answer questions based on information stored in its internal database 📂❓




# HOW TO 🧑‍🏫
## HOW TO INSTALL
### Installing catkin
1. sudo-apt-install python3-catkin-tools
2. sudo apt install -y python-rosdep python-rosinstall python-rosinstall-generator python-
wstool build-essential ros-melodic-catkin python-catkin-tools

### Installing ROS
#### Setup sources.list and keys
1. sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
2. sudo apt install curl # if you haven't already installed curl curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc |
3. sudo apt-key add -
#### Installation and environment setup
1. sudo apt update
2. sudo apt install ros-noetic-desktop-full
3. source /opt/ros/noetic/setup.bash
4. echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc source ~/.bashrc
#### To use with python3
1. sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
2. sudo apt install python3-rosdep
3. sudo rosdep init
4. rosdep update
5. sudo apt-get install ros-noetic-catkin python-catkin-tools

### Installing Rasa 
1. sudo apt update
2. sudo apt install python3-pip
3. pip3 install pip
4. pip3 install rasa
5. pip3 install rasa\[spacy\]
6. pip3 install rasa\[transformers\]

### Installing audio module: 
1. sudo apt install -y libasound-dev ffmpeg portaudio19-dev libportaudio2 libportaudiocpp0
2. python3 -m pip install pyaudio speechrecognition librosa sounddevice python_speech_features scipy soundfile

### Installing detection module:
1. sudo apt install -y ros-noetic-vision-msgs
2. python3 -m pip install tensorflow rosnumpy


### Installing NaoQi (Pepper)
1. sudo apt update && sudo apt install -y git
2. cd$HOME
3. wget https://github.com/gdesimone97/cogrob_pepper_nodes/releases/download
/requirements/install.bash -O install.bash
4. bash install.bash
5. cd $HOME/catkin_ws
6. catkin build
7. source devel/setup.bash



## HOW TO RUN
### Activate Pepper nodes
1. connect on the same pepper's net
2. roslaunch pepper_nodes pepper_bringup.launch nao_ip:=x.x.x.x



## How to visualize images on Pepper's tablet

### Configure webserver on your PC
1. Install Flask:
    - `python3 -m pip install Flask`
2. Configure the webserver:
    - [Flask Tutorial](https://flask.palletsprojects.com/en/stable/tutorial/layout/)
3. Load the webview provided in the lesson

### Send images to webview

1. Start the tablet node such as in [https://github.com/gdesimone97/cogrob_pepper_nodes/blob/main/src/pepper_nodes/src/tablet_node.py](https://github.com/gdesimone97/cogrob_pepper_nodes/blob/main/src/pepper_nodes/src/tablet_node.py)
2. Load the webview on Pepper tablet using the `load_url` method.
    - Example: [https://github.com/gdesimone97/cogrob_pepper_nodes/blob/main/src/examples/src/tablet_example.py](https://github.com/gdesimone97/cogrob_pepper_nodes/blob/main/src/examples/src/tablet_example.py)
    - Pay attention you have to send a request to your webserver in the format: `http://<WEB_SERVER_IP:<WEB_SERVER_PORT>`
3. Call the `execute_js` ROS service sending the image in base64
    - Example code:

```python
def show_image(self, img: np.ndarray):
        # Get the numpy array image as input
        video_script = 'document.getElementById("rtv").src="data:image/png;base64, {}";'
        image_base64 = base64.b64encode(img).decode('UTF-8') # From numpy array to base64 string
        script = video_script.format(image_base64)
        ## <Call the execute_js ROS Service sending the script varible defined above>
```


![Alt text](https://corporate-internal-prod.aldebaran.com/themes/custom/softbank/images/360/pepper.png)
