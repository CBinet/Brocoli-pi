# WebPI

# Installation

### Install git :
Git is installed by default on most raspberrys.
If git is not installed, you can install it with the following command :
```sh
sudo apt-get install git --y
```

### Clone the repository :
Navigate where you want to create the folder and clone the repository :
```sh
git clone https://github.com/WebPI.git
```

### Launch WebPi
Launch the server :
```sh
python server.py
```

### Extras - Setup autorun on bootup
If you want to start the server automatically when
you boot up your raspberry, you can modify the .profile file
with the following command :
```sh
sudo nano ~/.profile
```
This will open your terminal file editor. Add the following line
at the end of the file :
```sh
python <where-your-server.py-is-located>/server.py
```
Then press CTRL+X, Y to save and quit the file editor.

**Example** : if your git repository is located in your
home folder. If you want the latest version of *WebPi*,
then start the server and also add a greeting message, 
you would do something like this :
```sh
echo Greetings, human.
cd ~/
git pull origin master
python server.py
```

# Using WebPi
To run the server
```sh
python server.py
```

# Modules

### GPIOControls

**Classes** :
- **Output** : *Single output pin*
- **Group** : *Group of output pins*

**Usage** : 
```py
# Instanciate an output at location '17'
# with label "Red Light".
output = Output(17, "Red Light")

# Toggles the voltage of 'output'
output.toggle()

# ...

# Instanciate a group controlling 'outputs' with
# the label "LED group"
group = Group(0, outputs, "LED group")

# This will toggle the voltage of the outputs
# of the group.
group.toggle()
```


**Routes** :
- GET/ outputs : *Returns informations of current binded outputs*
- GET/ outputs/:id : *Returns information of the output at 'id' location*
- GET/ outputs/:id/toggle : *Toggle the voltage of the output at 'id' location*
- GET/ groups : *Returns informations of current binded groups*
- GET/ groups/:id : *Returns information of the group 'id'*
- GET/ groups/:id/toggle : *Toggle the voltage of the output of group 'id'*

**Example response** :

*GET/ outputs* :
```json
{
  "results": [
    {
      "id": 17,
      "info": "Red Light",
      "state": false
    },
    {
      "id": 18,
      "info": "Green Light",
      "state": false
    },
    {
      "id": 19,
      "info": "Yellow Light",
      "state": false
    }
  ]
}
```

### Weather

Working on it :) This is what is available at the moment.

**Routes** :
- GET/ weather/current?city='city' : *Returns current's weather of 'city'*
- GET/ weather/forecast?city='city' : *Returns the comming days' weather of 'city'*

**Example response** :
*GET/ weather/today?city=Quebec* :
```json
{
  "precip_mm": 1.7,
  "last_updated": "2017-04-12 03:15",
  "wind_degree": 50,
  "wind_kph": 15.1,
  "is_day": 0,
  "temp_f": 36.3,
  "vis_miles": 5,
  "temp_c": 2.4,
  "humidity": 98,
  "last_updated_epoch": 1491981306,
  "cloud": 0,
  "feelslike_c": -1.5,
  "wind_mph": 9.4,
  "feelslike_f": 29.3,
  "wind_dir": "NE",
  "pressure_mb": 1021,
  "vis_km": 9.3,
  "precip_in": 0.07,
  "pressure_in": 30.6,
  "condition": {
    "text": "Clear",
    "code": 1000,
    "icon": "//cdn.apixu.com/weather/64x64/night/113.png"
  }
}
```