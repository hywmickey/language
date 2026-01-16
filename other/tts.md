


保存谷歌翻译音频

似乎当你第一次将鼠标移到扬声器图标上时，谷歌翻译会检索到一个包含音频编码版本的JSON文件。我认为这篇文章是将其转化为实际音频的关键：

https://cloud.google.com/text-to-speech/docs/base64-decoding

所以实验：

（1） 右键单击以batchexecute开头的请求？然后单击“在新选项卡中打开”，然后从“下载”对话框中保存文件（Firefox从Content-Disposition标头中获取名称response.bin，您可以在保存时或打开之前添加.json）

（2） 在文本编辑器中打开.json文件，并从文件开头删除以下内容——请注意，我假设这个数字会根据音频有效负载的大小而变化：

```

)]}'

13156 [["wrb.fr","jQ1olc", "[\"

```

（3） 在文件底部，删除以下内容，这些内容可能会有所不同：

```

\"]\n",null,null,null,"generic"] ] 58 [["di",110] ,["af.httprm",109,"2935967112318335285",7] ] 28 [["e",4,null,null,13257] ]

```
（4） 保存文件

（5） 打开命令提示符（cmd.exe），导航到正确的文件夹，然后运行

`certutil -decode response.bin.json testaudio.mp3`


```

在浏览器的【网络】请求中查看下面链接的返回数据
https://translate.google.com/_/TranslateWebserverUi/data/batchexecute

要将 base64 内容解码到音频文件，请执行以下操作：

Linux：
    $ base64 SOURCE_BASE64_TEXT_FILE -d > DESTINATION_AUDIO_FILE
MacOS：
    $ base64 --decode -i SOURCE_BASE64_TEXT_FILE > DESTINATION_AUDIO_FILE
Windows：
   certutil -decode SOURCE_BASE64_TEXT_FILE DESTINATION_AUDIO_FILE
参考：
    对使用 Base64 编码的音频内容进行解码： https://docs.cloud.google.com/text-to-speech/docs/base64-decoding?hl=zh-cn#linux

```

---

使用gTTS命令创建音频文件

```
安装gTTS库：
方法一：
pip3 install gTTS

方法二：
mkdir gtts
python3 -m venv ./gtts
source ./gtts/bin/activate
python3 -m pip install gTTS
gtts-cli 'hello' --output hello.mp3
```
