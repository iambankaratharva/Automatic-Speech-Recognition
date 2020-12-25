# Automatic-Speech-Recognition
Speaker Independent Automatic Speech Recognition for continuous audio.

## Documentation for End User
Pre-requirements – 
Python 3.6 and above required for the execution of the model.

Weights should be downloaded which are provided with the documentation.

### Python Libraries required: pip3 install lib_name
pandas, numpy, librosa, matplotlib, IPython, os, sys, scipy, sklearn, time, tensorflow, keras, pydub, sounddevice, soundfile, pysndfx, python_speech_features

The all_labels.npy file should be downloaded.

### The user should follow the following steps - 
1.	The user should begin with the basic step of importing all the required libraries and downloading all the dependencies which are specified in the beginning of the code.

2.	Once the weights are downloaded onto the system where the model is to be executed, it should be loaded into the model with the following lines of code.
model = load_model('Path where the weights file is downloaded)

3.	As the model is trained on the 30 words which will be used for classification, they should be stored into a variable (namely labels) for further predictions.
labels = ['eight', 'sheila', 'nine', 'yes', 'one', 'no', 'left', 'tree'   , 'bed', 'bird', 'go', 'wow', 'seven', 'marvin', 'dog', 'three', 'two', 'house', 'down', 'six', 'five', 'off', 'right', 'cat', 'zero', 'four', 'stop', 'up', 'on', 'happy']

4.	The user should download the file all_labels.npy which stores all the word labels. And then load it into the working directory.
all_labels = np.load(os.path.join("Path of the file all_labels.npy"))

5.	Following these initialisations, the user should then encode this categorical data with the help of the LabelEncoder().
le = LabelEncoder()	

6.	The system performs the predictions with the help of the defined predict (audio,n,k=0.6) function. The output of this function is the predicted class. Along with this, the function writes the predicted output along with the time stamp into a text file whose path is to be mentioned. The threshold can be changed by passing a value for the parameter k.
Predict function - def predict(audio,n,k=0.6):
Time stamp –
UTC = pytz.utc 
IST = pytz.timezone('Asia/Kolkata')

Output file – 
f=open(r'Path of the file where output will be stored' + '{0}'.format(n)+'.txt', 'a')

7.	The audio file which is to be tested needs to be normalised. This is done with the help of the match_target_variable(). This function returns a value change_n_dBFS which is used for normalisation. Normalisation is done with the use of apply_gain() function.
def match_target_amplitude(aChunk, target_dBFS):
aChunk.apply_gain(change_in_dBFS)

8.	For the model to convert the given audio file into .wav format the following lines of code should be executed. For the AudioSegment() function to be executed the user needs to download FFMPEG onto his system. Below is the link to git clone it. https://ffmpeg.org/download.html#build-windows (No need of FFMPEG for Google Colab)

9.	After cloning it onto the system the user needs to move the ffmpeg.exe and ffprobe.exe files to some other file as they are necessary for conversion of audio files.

10.	The model is executed on the calling of the Speech_Recognition function. The function takes in 3 parameters srs,dst and min_silence_len. The min_silence_len  is set to default value 200 and can be changed while calling.
Speech_recognition(src1,dst1,min_silence_len = 200)

11.	The src and dst variable are the file paths where the user has the audio files to be tested and where he wants to store the .wav files for predcitions. 

12.	Following to this, the dBFS is calculated and the continuous audio is split into individual speech commands. The individual speech commands need to be exported to some directory which is to be mentioned by the user. 
 print("Exporting chunker{0}.wav.".format(i))
 k = normalized_chunk.export(
 r'path to store individual speech commands' .format(i),
 bitrate = "192k",	
 format = "wav"

13.	The audio samples are then resampled to 8000Hz and the final predictions are made. For resampling, we need to mention the directory where individual speech commands are stored.
filepath=r'Path of individual speech commands'.format(i)
print(filepath)	

14.	Lastly the .txt file where the predictions exist is then converted to a .csv file.
dataframe1 = pd.read_csv(r"Path of the prediction file with format .txt ".format(n),header=None) 
dataframe1.to_csv(r"Path to store the converted .csv file ".format(n),index = None)
