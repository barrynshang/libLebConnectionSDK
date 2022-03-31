# 快直播传输层SDK - libLebConnectionSDK


## 1. 主要功能
  - 音视频拉流，兼具优异的低延迟性能和抗弱网能力
  - 视频支持H264、H265和AV1，支持B帧，视频输出格式为视频帧裸数据(H264/H265为AnnexB，AV1为OBU)
  - 音频支持AAC和OPUS，音频输出格式为音频帧裸数据
  - 支持Android、iOS、Windows、Linux和Mac平台


## 2. SDK接口调用流程
   
  ![image](https://github.com/tencentyun/libLebConnectionSDK/blob/main/docs/api_calling_sequence.png)

## 3. SDK接口说明
### 3.1 基础接口说明
- 创建快直播连接
```c
LEB_EXPORT_API LebConnectionHandle* OpenLebConnection(void* context, LebLogLevel loglevel);
```
- 注册回调函数
```c
LEB_EXPORT_API void RegisterLebCallback(LebConnectionHandle* handle, const LebCallback* callback);
```
- 开始连接拉流
```c
LEB_EXPORT_API void StartLebConnection(LebConnectionHandle* handle, LebConfig config);
```
- 停止连接
```c
LEB_EXPORT_API void StopLebConnection(LebConnectionHandle* handle);
```
- 关闭连接
```c
LEB_EXPORT_API void CloseLebConnection(LebConnectionHandle* handle);
```

### 3.2 回调接口说明
```c
typedef struct LebCallback {
  // 日志回调
  OnLogInfo onLogInfo;
  // 视频信息回调
  OnVideoInfo onVideoInfo;
  // 音频信息回调
  OnAudioInfo onAudioInfo;
  // 视频数据回调
  OnEncodedVideo onEncodedVideo;
  // 音频数据回调
  OnEncodedAudio onEncodedAudio;
  // MetaData回调
  OnMetaData onMetaData;
  // 统计信息回调
  OnStatsInfo onStatsInfo;
  // 错误回调
  OnError onError;
} LebCallback;
```
Notes：详细数据结构定义请见头文件**leb_connection_api.h**

### 4. FFmpeg集成
SDK提供FFmpeg webrtc demuxer源码：webrtc_demuxer.c，可以实现FFmpeg快直播拉流和媒体处理，以及ffplay播放

FFmpeg配置编译可以参考：[快直播传输层SDK FFmpeg集成说明](https://docs.qq.com/doc/DWExGWnZacnZWR2JW)

### 5. 播放器集成示例
  ![image](https://github.com/tencentyun/libLebConnectionSDK/blob/main/docs/player_framework.png)
  具体可以参考：[基于ijkplayer的快直播传输层SDK应用实践](https://mp.weixin.qq.com/s/f3ct29ydzAjdJ1fIdOmHmQ)

