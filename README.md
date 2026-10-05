# 千星奇域音效与 AI 听感描述

本资料收录 **1,997 条音效索引**，每条包含中文短描述和详细描述。音效与描述具有不同来源：名称、类别和资源ID来自游戏配置，描述由AI根据音频生成。

## 音效来源

音频来自《原神》千星奇域（BeyondUGC）的游戏资源包，按声音媒体从WEM解码为WAV。资源ID和中文名称依据公开的 [DimbreathBot/AnimeGameData](https://github.com/DimbreathBot/AnimeGameData) 配置快照，固定提交 `792978e5503ecfba73dcb3562ed44a0d35a2abe2`（2026-10-01）：

- [音效配置表](https://github.com/DimbreathBot/AnimeGameData/blob/792978e5503ecfba73dcb3562ed44a0d35a2abe2/ExcelBinOutput/BeyondAudioSFXExcelConfigData.json)
- [中文TextMap](https://github.com/DimbreathBot/AnimeGameData/blob/792978e5503ecfba73dcb3562ed44a0d35a2abe2/TextMap/TextMapCHS.json)
- Wwise事件结构参考：[bnnm/wwiser](https://github.com/bnnm/wwiser)

映射链：配置ID → 事件名称 → Wwise FNV-1事件ID → Event → Play Action → Sound → sourceID → WEM → WAV。对应关系依据资源引用链建立，没有按文件时长猜测映射。

范围为该配置快照中的全部1,997条音效，不含音乐，不保证覆盖未来更新。WAV对应原始声音媒体，没有叠加Wwise事件音量、总线效果或游戏播放环境。

## 描述来源

描述于2026-10-05通过阿里云百炼DashScope的 **`qwen3.8-omni-flash`** 实时API生成。关闭思考，仅返回中文文本；同一音频分别请求短、长两版，模型没有收到资源名称、分类、ID或游戏出处。

**这些描述是AI生成的听感解释，不是游戏官方描述，也未经人工逐条听审。** 可能存在错误或多义解释，短、长两版也可能对音色产生不同判断。需要精确判断时，应试听音频。描述不能替代音频输入能力。

短描述提示词（max_tokens=128）：

> 请只用一句不超过35个汉字的中文描述这段音效的主要音色及变化。不要解释，不猜测游戏出处或录制环境。

详细描述提示词（max_tokens=384）：

> 请用80到120个汉字描述这段音效，重点说明起音、主体音色、声音层次、强弱或音高变化以及尾音。只描述能听到的特征，不猜测游戏出处、录制设备、具体场所或制作过程；无法判断的细节不要编造。只输出一段中文。

字数是提示目标，未强制截断或改写模型输出。最初失败的3条已补齐：10003的完整音频转16kHz单声道后请求；50870（约84毫秒）与50908（约48毫秒）转16kHz单声道，并在两端补静音到1秒后请求。只改变提交模型的副本，原WAV、时长与校验值保持不变；没有循环、时间拉伸或增益归一化。

## 数据格式

本文是完整可读目录；`catalog.json`包含来源、生成提示和所有条目；`音效目录.jsonl`每行一条，适合检索；`长短描述对照.csv`使用UTF-8 BOM。

| 字段 | 含义 |
|---|---|
| id | 游戏配置资源ID |
| name / category | 配置中文名称与原库分类 |
| audio_file | 音频相对路径，如audio/环境/10008_环境_雷声_01.wav |
| duration_seconds | 原WAV解码时长，单位秒 |
| wem_sha256 | 原库索引提供的WEM媒体文件SHA256校验值 |
| wav_sha256 | 本次直接计算的WAV文件SHA256校验值 |
| short_description | 模型生成的短听感描述 |
| detailed_description | 模型生成的详细听感描述 |
| description_status | complete表示长短两版均已生成，不表示内容准确性评级 |
| description_input_processing | 仅3条特殊输入提供转换记录；其余直接提交原WAV |

本目录包含全部1,997个WAV及独立全库试听网页。下载并保留目录结构后，直接打开`index.html`，或在Windows双击`打开试听.cmd`，即可离线搜索、筛选、试听、下载音效并对照长短描述，无须安装程序、运行服务或提供API密钥。所有音频路径相对资料根目录；请保留`audio/`目录与网页的相对位置。网页已内置描述数据，不依赖在线接口。AI可先按ID、分类或声音特征检索，再读取相关条目，无须一次载入全文。

本资料是非官方整理。游戏音效的权利属于相关权利人；描述来源于AI生成，不代表官方授权，本资料没有为游戏音频授予开源许可。


完整条目见 [千星奇域音效库_AI通用文档.md](千星奇域音效库_AI通用文档.md)。
