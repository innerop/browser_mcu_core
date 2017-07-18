# Browser MCU Core

* Browser MCU Core is MCU library using a browser for video/audio processing
* Browser MCU Core is designed for MediaStreams from WebRTC
* Signaling and handling of PeerConnection are not a part of Browser_MCU Core
* Browser MCU Core is a part of Browse MCU Series
* --
* Browser MCU Core はブラウザの映像/音声処理を活用した、MCUライブラリです
* Browser MCU Core は WebRTC でやり取りする MediaStream を扱うために作成されています
* シグナリングや PeerConnection の処理は、Browser MCU Core には含まれていません
* Browser MCU Core は Browse MCU シリーズの一部です

## Confirmed Environment / 動作確認環境

* Chrome  58.0.3029.110 (64-bit) for MacOS X
* Firefox 54.04 (64-bit) for MacOS X


## Samples / サンプル

### video mix sample

* [view source on GitHub](https://github.com/mganeko/browser_mcu_core/blob/master/mix_sample.html) / [GitHubでソースを見る](https://github.com/mganeko/browser_mcu_core/blob/master/mix_sample.html)
* [try GitHub pages](https://mganeko.github.io/browser_mcu_core/mix_sample.html) / [GitHub pages で試す](https://mganeko.github.io/browser_mcu_core/mix_sample.html)

#### How to use sample / サンプル操作手順

* Prepare
  * copy mix_sample.html, js/browser_mcu_core.js to your local web server
* Open http://localhost:your_port/your_path/mix_sample.html with Chrome/Firefox
* Click [Add Video] Button and allow access to Camera / Michrophone
* Click [Add Video] Button many times (up to 25)
* Then, videos are mixed
* --
* 事前準備
  * ローカルマシンのWebサーバーに、mix_sample.html, js/browser_mcu_core.js を配置します
  * Chrome か Firefox 
* Chrome/Firefoxブラウザで http://localhost:あなたのポート/あなたのパス/mix_sample.html を開きます
* [Add Video]ボタンを押します。カメラ/マイクのアクセス許可を求められたら、許可してください
* [Add Video]ボタンを何度か押します。（最大25）
* 映像/音声が合成されます

## Usage / 利用方法

#### Prep

* Load browser_mcu_core.js in HTML

```
<script src="js/browser_mcu_core.js"></script>
```

#### Initialization / 初期化

* new object of BrowserMCU
* set Canvas to use for mixing video
* set div element to use as container of videos to mix
* set audio mode (AUDIO_MODE_NONE, AUDIO_MODE_MINUS_ONE, AUDIO_MODE_ALL)

#### Start Mix Video/Audio / 合成の開始

* call startMix()
* call getMixStream()
* when AUDIO_MODE_NONE
  * call addRemoteVideo()
* when AUDIO_MODE_ALL
  * call addRemoteAudio()
  * call addRemoteAudio()
* when AUDIO_MODE_MINUS_ONE
  * call prepareMinusOneStream() for each peer (stream)
  * call addRemoteAudio()
  * call addRemoteAudioMinusOne()

#### Stop  Mix Video/Audio / 合成の停止

* call removeAllRemoteAudio() / removeAllRemoteAudioMinusOne()
* call removeAllRemoteVideo()
* call stopMix()


### Code Samples / コード例

```
  let mcu = new BrowserMCU();
  mcu.setCanvas(document.getElementById('mix_canvas'));
  mcu.setContainer(document.getElementById('video_container');
  mcu.setAudioMode(BrowserMCU.AUDIO_MODE_ALL); //   AUDIO_MODE_NONE, AUDIO_MODE_MINUS_ONE, AUDIO_MODE_ALL
  mcu.startMix();
  let mixStream = mcu.getMixStream();

  mcu.addRemoteVideo(remoteStream1);
  mcu.addRemoteAudio(remoteStream1);

  mcu.addRemoteVideo(remoteStream2);
  mcu.addRemoteAudio(remoteStream2);

  mcu.addRemoteVideo(remoteStream3);
  mcu.addRemoteAudio(remoteStream3);  
```

### NOTE / 注意

* mixed video will not be updated when window/tab is hidden
  * window/tab do not have to be shown on headless browser
* ウィンドウ/タブが完全に隠れていると、合成した映像が更新されません
  * ヘッドレスブラウザの場合は、画面が見えなくても問題ありません

## License / ライセンス

* Browser MCU Core is under the MIT license
* Browser MCU Core はMITランセンスで提供されます



