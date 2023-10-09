# mdict-utils

本代码库是从 [liuyug/mdict-utils](https://github.com/liuyug/mdict-utils) fork 而来。主要是为了解决这些问题：
1. pack时控制key是否再次排序
2. 资源key的开头和路径分隔符不合理

其他保持原框架的功能和使用方式不变，详细参见 [liuyug/mdict-utils 说明文档](./OLD-README.rst)

## pack时控制key是否再次排序

*原来的问题*

在进行 pack 打包时，原来的 [liuyug/mdict-utils](https://github.com/liuyug/mdict-utils) 会对key再次进行排序，而且这个排序会过滤掉特殊字符并按照本地规则进行排序（比如本地规则可能会认为 a和A 是一样的）。而是否进行排序也没有控制参数，如果外部已经排好序了，这里还是会打乱。

*修改后的方案*

增加 `sort` 参数：
* yes: 表示会进行排序，也是默认值
* no: 不进行排序

使用示例：
```bash
# 这是在 项目根路径下
python mdict_utils --title tmp/title.html --description tmp/description.html -a tmp/dict.txt --sort no tmp/dict.mdx

# 这是任何路径下
python /Users/jadyyang/code/ienglish/mdict-utils/mdict_utils --title /Users/jadyyang/code/ienglish/mdict-utils/tmp/title.html --description /Users/jadyyang/code/ienglish/mdict-utils/tmp/description.html -a /Users/jadyyang/code/ienglish/mdict-utils/tmp/dict.txt --sort no /Users/jadyyang/code/ienglish/mdict-utils/tmp/dict.mdx
```

## 资源key的开头和路径分隔符不合理

pack 打包 mdd文件时，key不合理：
1. 开头强制增加了 “\”
2. 路径分隔符使用了 “\”

现在分别进行了调整：
1. 开头不再增加 “\”
2. 路径分隔符使用了 “/”

使用示例：
```bash
# 这是在 项目根路径下
python mdict_utils --title tmp/title.html --description tmp/description.html -a tmp/mdd tmp/dict.mdd

# 这是任何路径下
python /Users/jadyyang/code/ienglish/mdict-utils/mdict_utils --title /Users/jadyyang/code/ienglish/mdict-utils/tmp/title.html --description /Users/jadyyang/code/ienglish/mdict-utils/tmp/description.html -a /Users/jadyyang/code/ienglish/ienglish-exporter/dict/source/ox_aleca_9/mdd-temp /Users/jadyyang/code/ienglish/mdict-utils/tmp/dict.mdd
```

注意：打包 mdd 文件时，最好不要加 `--sort no` 参数，还是需要排序的。因为读取文件时，并不能确定是什么顺序，所以还是需要排序的。
