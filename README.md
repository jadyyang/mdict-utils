# mdict-utils

本代码库是从 [liuyug/mdict-utils](https://github.com/liuyug/mdict-utils) fork 而来。主要是为了解决这些问题：
1. pack时控制key是否再次排序

其他保持原框架的功能和使用方式不变，详细参见 [liuyug/mdict-utils 说明文档](./OLD-README.rst)

## pack时控制key是否再次排序

*原来的问题*

在进行 pack 打包时，原来的 [liuyug/mdict-utils](https://github.com/liuyug/mdict-utils) 会对key再次进行排序，而且这个排序会过滤掉特殊字符并按照本地规则进行排序（比如本地规则可能会认为 a和A 是一样的）。而是否进行排序也没有控制参数，如果外部已经排好序了，这里还是会打乱。

*修改后的方案*

增加 `sort` 参数：
* yes: 表示会进行排序，也是默认值
* no: 不进行排序

python mdict_utils --title tmp/title.html --description tmp/description.html -a tmp/dict.txt tmp/dict.mdx --sort no
