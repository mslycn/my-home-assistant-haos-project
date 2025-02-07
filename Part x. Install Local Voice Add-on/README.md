## Voice Assistant Sofware
Under the Official add-ons section, search and install the following add-ons:
~~~
ESPHome

Whisper
Piper
openWakeWord
~~~

## Voice Assistant Hardware

1. seeedstrudio respeaker 2 or 4

https://wiki.seeedstudio.com/respeaker_lite_ha/

1. Local Voice control - Esp32+INMP441 esphome

https://github.com/Djelle/ESPHomeVoiceSatellite/blob/main/esphome-voice-satellite.yaml


Use OpenAI with Assist

# Install method
Install piper and whisper locally with Python virtual environment

Install piper and whisper locally with Docker

Install piper and whisper locally with Add on


## Project

- ESP32-S3-Box3B Ready-Made Project

https://esphome.io/projects/index.html




https://github.com/esphome/wake-word-voice-assistants/blob/main/esp32-s3-box-3/esp32-s3-box-3.yaml


- ESP32-S3-Box3-Custom Firmware

https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome

https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome/blob/main/instructions/installation%20guide.md

- I’ve just set up an ESP32-S3-BOX as well, flashed with Willow 

https://community.home-assistant.io/t/voice-assistant-faster-whisper-slow-and-ita-model-weak-any-support-about/689470

https://heywillow.io/


## 基础知识
在本地配置Assist和HomeAssistant语音助手，需要一些必要的组件。Assist的配置涉及Whisper、Piper以及openWakeWord这三个组件，它们被称为HomeAssistant的语音三件套。Whisper负责语音识别，Piper负责语音合成，openWakeWord负责检测唤醒词。

Assist配置教程
Assist的配置相对复杂，需要一定的技术背景。以下是一些基本的配置步骤：

安装HomeAssistant的语音三件套组件 ：首先，确保你已经安装了Whisper、Piper和openWakeWord。running  whisper/piper in docker on another host.。

配置语音识别 ：在HomeAssistant的配置文件中，你需要添加Whisper的相关配置。这通常涉及到指定模型路径、语言等参数。

配置语音合成 ：同样，在配置文件中添加Piper的配置。这包括选择语音模型、设置音量等。

设置唤醒词检测 ：openWakeWord的配置涉及到指定唤醒词模型、设置灵敏度等。

测试和调整 ：完成基本配置后，需要进行测试，确保语音识别、合成和唤醒词检测都能正常工作。根据测试结果，可能需要调整相关参数。

HomeAssistant配置教程
HomeAssistant的配置相对简单，但同样需要一些步骤：

安装HomeAssistant ：首先，你需要在你的设备上安装HomeAssistant。这可以通过多种方式完成，例如在树莓派上安装HomeAssistant OS。

配置网络和设备 ：安装完成后，通过浏览器访问HomeAssistant的Web界面。在这里，你可以配置网络设置，添加你的智能家居设备。

安装必要的集成 ：为了实现语音控制，你需要安装一些必要的集成，如HACS（Home Assistant Community Store）。这可以通过HomeAssistant的Supervisor界面完成。

配置语音助手 ：在HomeAssistant的配置文件中，添加语音助手的相关配置。这可能涉及到指定语音识别和合成服务。

测试和调整 ：完成配置后，进行测试，确保所有设备和功能都能正常工作。根据需要进行调整。

注意事项
硬件要求 ：确保你的设备有足够的性能和存储空间来运行HomeAssistant和相关的语音助手组件。

网络稳定性 ：语音助手的性能很大程度上依赖于网络连接。确保你的网络稳定，以获得最佳的使用体验。

隐私保护 ：语音助手会收集和处理语音数据。确保你了解并接受相关的隐私政策。

定期更新 ：定期更新HomeAssistant和相关的组件，以获得最新的功能和修复潜在的问题。

通过以上步骤，你应该能够在本地成功配置Assist和HomeAssistant语音助手，享受更加智能和便捷的家居体验。


**step 1. Install three add on**

**step 2. Wyoming Protocol Integration**

Next, go to the Integrations section and enable the Wyoming Protocol Integrations which should have been discovered.

**step 3. Test**

3.1 test piper

Test the voice generation by opening the Media Browser and going to the Text to Speech option and choosing “piper”. 

It should display a default sentence or two for testing purposes and have a language and voice selection option. Make sure the the voice it displays is the same one you installed in Piper and click “Say”. It may take a few seconds, but it should speak the line of text over the local speaker or headphones connected to your PC.

**step 4. create a new voice assistant**

Now comes the best part: creating the voice pipeline itself. Go to Settings, Voice assistants and click the button to create a new voice assistant, or you can edit the default one; either option will work.

Name the new voice assistant; I named mine “Local Voice”… Then select the Home Assistant Conversation Agent. For Speech to Text, select “faster-whisper”. For Text to Speech, select piper, your language, and the voice you set up for the piper add-on. For wake word engine, select “openwakeword”, then one of the default options. Then save the Voice Assistant.