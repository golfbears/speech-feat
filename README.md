# speech feature

This repository comes from wav2letter by facebook, which provides Automatic Speech Recognition Toolkit 
In this repository, speech feature extraction is modified to compile in linux alone, although depend on fftw and cblas.

some details about wav2letter refer to (https://github.com/facebookresearch/wav2letter) 

To get started with speech feature, please checkout or clone the source code, then 

mkdir build && cd build
cmake ..
make

The project provide a library with gtest for speech feature verification independently


## License

this project follow the license from wav2letter.
wav2letter++ is BSD-licensed, as found in the [LICENSE](LICENSE) file.
# speech-feat
