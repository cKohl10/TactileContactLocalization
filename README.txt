To use and edit the app, make sure you have Matlab App Designer installed. After cloning the repository 
with "git clone https://github.com/HIRO-group/TactileContactLocalization.git", run the main app window named
"ContactLocalizationApp.mlapp". 

The window will automatically search for a serial input connected to the host 
device streaming sensor values with a comma delimeter. This has only been tested with Arduino microcontrollers
but should still work as long as the serial input is what it is expecting.

######## Arduino Connection #########
skinObj -> Serial connection to the arduino. Use this when calling readSkin

########## Touch Data ###############
touchData ->  Struct containing all data needed for ML training from a data collection cycle
>> touchData.numTX ->                Number of transmitter wires
>> touchData.numRX ->                Number of receiver wires
>> touchData.numSensors ->           Number of sensors
>> touchData.numPL -> 		     Number of point logs
>> touchData.description ->          Name of data set

% Point Log Data: Sensor data from touching a location on the object
>> touchData.PL ->                   [1xpl] vector of all Point Log data sets, pl = number of point logs
>>>> touchData.PL.touchPos ->        [x,y,z] location of touch
>>>> touchData.PL.sensorStateRaw ->  [nxm] vector of all sensor data where n = sample size of point log and m = number of sensors
>>>> touchData.PL.sensorStateAvg ->  [1xm] vector of the averages of sensor data by sample size where m = number of sensors

% Calibration Point Log: Sensor data when no contact is made
>> touchData.CPL ->                  Single Calibration Point Log data sets
>>>> touchData.CPL.sensorStateRaw -> [nxm] vector of all sensor data where n = sample size of point log and m = number of sensors
>>>> touchData.CPL.sensorStateAvg -> [1xm] vector of the averages of sensor data by sample size where m = number of sensors

% Object model data for the object used in data collection
>> touchData.obj  -> 		     Struct for object data
>>>> touchData.obj.v ->		     [nx3] matrix of vertices that form each face verts  
>>>> touchData.obj.f ->		     [mx3] matrix of vertex locations in implied body frame
>>>> touchData.obj.fileLoc ->	     string of object file location from main directory
>>>> touchData.obj.Points ->      [nx3] matrix of discrete points along the surface

>> touchData.stl  ->             Struct for stl data
>>>> touchData.stl.fe ->         Struct containing all information of an fegeometry
>>>> touchData.stl.fileLoc ->	 string of object file location from main directory

% Sensor Locations
>> touchData.sns ->		     [1xn] matrix of sensor structs
>>>> touchData.sns.posPred ->	     [x,y,z] matrix of predicted sensor location
>>>> touchData.sns.posReal -> 	     [x,y,z] matrix of real sensor locations (if given)

