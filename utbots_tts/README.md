## Setup
- ### Setup Mimic3 TTS (https://github.com/MycroftAI/mimic3)
    ```bash
    # Download mimic3
    cd ~/Downloads
    wget https://github.com/MycroftAI/mimic3/releases/download/release%2Fv0.2.4/mycroft-mimic3-tts_0.2.4_amd64.deb

    # Install with apt
    sudo apt install ./mycroft-mimic3-tts_0.2.4_amd64.deb

    # Test Mimic3 (it should take a small time to download the model)
    mimic3 --voice en_US/hifi-tts_low 'Hello world' | aplay

    # Test the Mimic3 ROS node
    rosrun utbots_voice ros_tts_mimic.py
    rostopic pub /voice/tts/text std_msgs/String 'Hello world' # (in another terminal)
    ```

- ### Coqui TTS (https://github.com/coqui-ai/TTS)
    ```bash
    # Install TTS
    python3 -m pip install TTS

    # Install Python dependencies
    python3 -m pip install playsound

    # Download models (they will be placed at ~/.local/share/tts/)
    cd /tmp
    tts --text "This command will download models" --model_name "tts_models/en/ljspeech/tacotron2-DDC" --vocoder_name "vocoder_models/en/ljspeech/hifigan_v2" --out_path speech.wav
    tts  --text "Isso vai baixar os modelos" --model_name tts_models/multilingual/multi-dataset/your_tts  --speaker_wav speech.wav --language_idx "pt-br"

    # Test the Coqui TTS ROS node
    rosrun utbots_voice ros_tts_coqui.py
    rostopic pub /voice/tts/text std_msgs/String 'Olá mundo!' # (in another terminal)
    ```