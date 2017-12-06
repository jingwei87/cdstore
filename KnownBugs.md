# 问题汇总
## 公共
1. README文件格式不是markdown导致解析不正常
2. README文件没写出来：leveldb需要snappy支持、gf-complete需要预先安装（安装方法也没有）、运行效果描述不清。

## client
1. 下载完成后文件被存储在了/client/decode_copy中，且没有在README中说明，使用困难。
2. 下载文件需要读取到原文件才可以下载（与REED一样）-main.cc中处理逻辑不对