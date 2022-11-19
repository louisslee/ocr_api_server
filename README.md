# HA addon: ddddocr_api

本项目fork自https://github.com/sml2h3/ocr_api_server, 为方便HA应用开发，做成了HA addons.


通过如下方式clone后，在HA webUI中的加载项-》加载项商店就可以找到了。

```bash
cd /addons
git clone https://github.com/louisslee/ocr_api_server.git
```


## 接口使用方法（更详细使用方式，请看原repo)
```python
# 1、测试是否启动成功，可以通过直接GET访问http://{host}:{port}/ping来测试，如果返回pong则启动成功

# 2、OCR/目标检测请求接口格式：

# http://{host}:{port}/{opt}/{img_type}/{ret_type}
# opt：操作类型 ocr=OCR det=目标检测 slide=滑块（match和compare两种算法，默认为compare)
# img_type: 数据类型 file=文件上传方式 b64=base64(imgbyte)方式 默认为file方式
# ret_type: 返回类型 json=返回json（识别出错会在msg里返回错误信息） text=返回文本格式（识别出错时回直接返回空文本）

# 例子：

# OCR请求
# resp = requests.post("http://{host}:{port}/ocr/file", files={'image': image_bytes})
# resp = requests.post("http://{host}:{port}/ocr/b64/text", data=base64.b64encode(file).decode())

# 目标检测请求
# resp = requests.post("http://{host}:{port}/det/file", files={'image': image_bytes})
# resp = requests.post("http://{host}:{port}/det/b64/json", data=base64.b64encode(file).decode())

# 滑块识别请求
# resp = requests.post("http://{host}:{port}/slide/match/file", files={'target_img': target_bytes, 'bg_img': bg_bytes})
# jsonstr = json.dumps({'target_img': target_b64str, 'bg_img': bg_b64str})
# resp = requests.post("http://{host}:{port}/slide/compare/b64", files=base64.b64encode(jsonstr.encode()).decode())
```
