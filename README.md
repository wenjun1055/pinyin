Pinyin [![Build Status](https://travis-ci.org/overtrue/pinyin.svg?branch=master)](https://travis-ci.org/overtrue/pinyin)
======

基于CC-CEDICT词典的中文转拼音工具, 更准确的汉字转拼音解决方案。 [CC-CEDICT](http://cc-cedict.org/wiki/).

```php
use \Overtrue\Pinyin\Pinyin; //请注意1.x系列的命名空间不同

echo Pinyin::pinyin('带着希望去旅行，比到达终点更美好');
// dài zhe xī wàng qù lǔ xíng bǐ dào dá zhōng diǎn gèng měi hǎo

//多音字
// 了
Pinyin::pinyin('了然'); // liǎo rán
Pinyin::pinyin('来了'); // lái le

// 还
Pinyin::pinyin('还有'); // hái yǒu
Pinyin::pinyin('交还'); // jiāo huán

// 什
Pinyin::pinyin('什么'); // shén me
Pinyin::pinyin('什锦'); // shí jǐn

// 便
Pinyin::pinyin('便当'); // biàn dāng
Pinyin::pinyin('便宜'); // pián yí

// 剥
Pinyin::pinyin('剥皮'); // bāo pí
Pinyin::pinyin('剥皮器'); // bō pí qì

// 不
Pinyin::pinyin('赔不是'); // péi bú shi
Pinyin::pinyin('跑了和尚，跑不了庙'); // pǎo le hé shàng , pǎo bù liǎo miào

// 降
Pinyin::pinyin('降温'); // jiàng wēn
Pinyin::pinyin('投降'); // tóu xiáng

// 都
Pinyin::pinyin('首都'); // shǒu dū
Pinyin::pinyin('都什么年代了'); // dōu shén me nián dài le

// 乐
Pinyin::pinyin('快乐'); // kuài lè
Pinyin::pinyin('音乐'); // yīn yuè

// 长
Pinyin::pinyin('成长'); // chéng zhǎng
Pinyin::pinyin('长江'); // cháng jiāng

// 难
Pinyin::pinyin('难民'); // nàn mín
Pinyin::pinyin('难过'); // nán guò
...

```


# 安装
1. 使用 Composer 安装:
	```
	composer require overtrue/pinyin:2.*
	```
	或者在你的项目composer.json加入：
	```javascript
	{
	    "require": {
	        "overtrue/pinyin": "2.*"
	    }
	}
	```

2. 直接下载文件 `src/Pinyin/Pinyin.php` 引入到项目中。


# 使用

```php
<?php
use \Overtrue\Pinyin\Pinyin;

//获取拼音
echo Pinyin::pinyin('带着希望去旅行，比到达终点更美好');
// dài zhe xī wàng qù lǔ xíng bǐ dào dá zhōng diǎn gèng měi hǎo

//获取首字母
echo Pinyin::letter('带着希望去旅行，比到达终点更美好');
// D Z X W Q L X B D D Z D G M H
```

## 设置

|      选项      | 描述                                                |
| -------------  | --------------------------------------------------- |
| `delimiter`    | 分隔符，默认为一个空格 ' '                          |
| `traditional`  | 繁体                                                |
| `accent`       | 是否输出音调                                        |
| `letter`       | 只输出首字母，或者直接使用`Pinyin::letter($string)` |
| `only_chinese` | 只保留`$string`中中文部分                           |


*全局设置：*  `Pinyin::set('delimiter', '-');`

*临时设置：*  `Pinyin::pinyin($word, $settings)` 在调用的方法后传参

example:

```php

Pinyin::set('delimiter', '-');//全局
echo Pinyin::pinyin('带着希望去旅行，比到达终点更美好');

// dài-zhe-xī-wàng-qù-lǔ-xíng-bǐ-dào-dá-zhōng-diǎn-gèng-měi-hǎo
```
```php

$setting = [
	    'delimiter' => '-',
	    'accent'    => false,
	   ];

echo Pinyin::pinyin('带着希望去旅行，比到达终点更美好', $setting);//这里的setting只是临时修改，并非全局设置

// dai-zhe-xi-wang-qu-lu-xing-bi-dao-da-zhong-dian-geng-mei-hao
```

```php
Pinyin::set('accent', false);
echo Pinyin::pinyin('带着希望去旅行，比到达终点更美好');

// dai zhe xi wang qu lu xing bi dao da zhong dian geng mei hao
```

# 在Laravel中使用

```shell
composer require overtrue/pinyin:2.*
```
在laravel配置文件中`app.php`里`providers`里加入:
```php
'Overtrue\Pinyin\PinyinServiceProvider',
```
然后看起来可能是这样：
```php
	'providers' =>
		//...
		'Illuminate\Validation\ValidationServiceProvider',
		'Illuminate\View\ViewServiceProvider',
		'Overtrue\Pinyin\PinyinServiceProvider',
	],
```

然后你可以添加配置文件：`config/pinyin.php`(_注意：此项为可选，如果不需要设置则不用创建此文件_):
```php
<?php

return [
	'delimiter' => '-',
	'accent' => false,
	//...
];
```
以上的设置会是全局的设置，如需临时设置请在方法里传参，例如:
```php
Pinyin::letter('您好世界', ['delimiter' => '-']); //N-H-S-J
```

### 使用
与上面的使用方法一样：

```php
use \Overtrue\Pinyin\Pinyin;

//...

$pinyin = Pinyin::pinyin("带着希望去旅行，比到达终点更美好");

```

# 说明
- 1.x的命名空间是`\Overtrue`，2.x的命名空间是`\Overtrue\Pinyin`（之前的写法不规范 :see_no_evil:）

# TODO
- [x] 添加获取首字母；
- [x] 支持繁体；
- [x] 添加补充词典；
- [x] 添加音频表，根据音频提高未匹配词典时多音字准确度；
- [x] 添加Laravel的serviec provider.

# Contribution
欢迎提意见及完善补充词库 `src/Pinyin/data/additional.php`! :kiss:

# 参考
- [CC-CEDICT](http://cc-cedict.org/wiki/)
- [現代漢語語音語料庫](http://mmc.sinica.edu.tw/intro_c_01.html)
- [汉典](http://www.zdic.net/)

# License

MIT
