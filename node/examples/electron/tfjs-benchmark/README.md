# Electron.js examples of tfjs-e2e-benchmark integration with WebNN node binding

In this app, you are able to test WebNN with OpenVINO backend for mobileNetV2 tflite model.

This app includes two tfjs-tflite builds,

- Official build, which is already included in tfjs-e2e-benchmark.
 1. url: https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-tflite@latest/dist/tf-tflite.js
 1. num_threads: supported, set to 1 means disabling multi-threads

- Custom build with WebNN Delegate, which is I added this time.
1. url: ./tflite-support/tflite_model_runner_cc_simd.js
1. multi_threads: not supported

## How to build app

1. Install dependencies: `$ npm install`
2. Build package: `$ npm run make`

## How to start app

**Prerequisites**: Download [OpenVINO 2021.4 Windows (x64)](https://registrationcenter-download.intel.com/akdlm/irc_nas/18320/w_openvino_toolkit_p_2021.4.752.exe) then follow the instructions [here](https://docs.openvino.ai/2021.4/openvino_docs_install_guides_installing_openvino_windows.html) to install it on Windows.

1. Start CMD, and set OpenVINO env vars: `$ C:\Program Files (x86)\Intel\openvino_2021\bin\setupvars.bat`
1. `$ npm start` or unzip app then launch tfjs_benchmark.exe file from CMD.

## How to run benchmark:

- For official tfjs-tflite(SIMD): Set `numRuns` and choose `tflite` backend, set `numThreads` to 1 then click “Run benchmark” button.
- For official tfjs-tflite(SIMD+MT): Set `numRuns` and choose `tflite` backend, set `numThreads` then click `Run benchmark` button. (For default multi-threads number you can check from dev-tools via `navigator.hardwareConcurrency / 2`.)

- For custom tfjs-tflite (WebNN Delegate):
1. Set `numRuns` and choose `tflite_webnn` backend.
2. For SIMD: unselect `enable webnn delegate` item then click `Run benchmark` button.
3. For OpenVINO: select `enable webnn delegate` and choose `cpu` or `gpu` in `webnn device preference` item, then click `Run benchmark` button.
