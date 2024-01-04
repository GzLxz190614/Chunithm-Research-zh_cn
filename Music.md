这是每个乐曲文件夹下的 ``root\app\data\AXXX\music\musicXXXX\Music.xml`` 文件的通用文档。

# 概述

``Music.xml`` 是与特定歌曲的谱面同在一个文件夹中的单一文件。该文件实质上是歌曲的元数据，为游戏提供了除谱面外几乎所有关于歌曲的信息。请注意，本文档不包括整个 XML 文件的结构，只包括其中的含义。要创建自己的 ``Music.xml`` 文件，请使用已有的文件作为模板，然后使用此处列出的规范。

本游戏中的 ``Music.xml`` 文件频繁使用了库存数组布局，如下所示：

```xml
<id></id>
<str></str>
<data />
```

任何对 "库存数组 "的引用都意味着值中存在这种数组格式，``<id>`` 和 ``<str>`` 标签已指定其值。``<data />``从不包含任何值，并始终采用这种格式。

# 标记

## dataName

``<dataname>``标记将有一个以父文件夹命名的值，通常是``musicXXXX``。

## formatVersion

``<formatVersion>``标记的值始终为 ``10000``。

## resourceVersion

``<resourceVersion>``标记始终包含一个库存数组，其``<id>``值为``0``，``<str>``值为``10000``。

## netOpenName

``<netOpenName>``标记包含一个未知值的存量数组。可能的解释是，这些值表示歌曲最初添加到游戏中的更新。

## disableFlag

``<disableFlag>``标签的值为``false``或``true``。启用 disableFlag 后，歌曲将不会出现在歌曲选择屏幕上。

## exType

``<exType>``标记的值为 0 到 2 之间的整数。如果值为 ``0``，歌曲将成为可在歌曲选择屏幕上选择的普通歌曲。如果值为``1``，歌曲将成为教程歌曲。数值为 ``2`` 时，歌曲将变为 WORLD'S END 歌曲。

## name

``<name>``标记包含一个库存数组，其中``<id>``值等于父文件夹名称的后 4 位数字（去掉前面的 0），``<str>``值包含将在游戏中显示的歌曲名称。

## rightsInfoName

``<rightsInfoName>``标记包含一个库存数组，其``<id>``值等于``root\app\data\AXXX\rightsInfo\rightsInfoXXXX``文件夹中相应的``rightsInfo``文件，去掉前面的0，以及一个``<str>``值，其中包含在``RightsInfo.xml``文件的``name``标记中显示的版权持有者名称（而非游戏中的名称）。如果歌曲不需要版权声明，则 ``<id>`` 的值为 ``-1``，``<str>`` 的值为 ``Invalid``。

## sortName

``<sortName>``标记以可按字母顺序排序的格式包含歌曲名称。所有拉丁字符均大写，所有标点符号和空格均被删除。对于日文标题，所有平假名和汉字都会转换成对应的片假名。

## artistName

``<artistName>``标记包含一个库存数组，其中``<id>``的值等于曲师的 ID，``<str>``的值是曲师在游戏中的名字。如果该曲师之前未在歌曲中使用过，则应赋予其与歌曲相同的 ID。如果以前使用过曲师，则应赋予与以前歌曲中使用的曲师 ID 相同的 ID。

## genreName

``<genreName>``标记包含一个``<list>``标记，该标记包含一个``<StringID>``标记，该标记包含一个存量数组，其中``<id>``值等于根据``root\app\data\AXXX\music``中的``GenreSort.xml``文件找到的有关版本的 ID，``<str>``值等于在``GenreSort.xml``文件中出现的版本名称。

## worksName

``<worksName>``标记包含一个库存数组，其中``<id>``值等于歌曲来源作品的 ID，``<str>``值等于相关作品的名称。这与 ``<artistName>`` 的规格相同。如果歌曲不需要版权声明，则``<id>``的值为``-1``，``<str>``的值为``Invalid``。

## jaketFile

``<jaketFile>``标记包含一个``<path>``标记，其值等于包含歌曲封面的文件名，通常与 Music.xml 文件位于同一目录。

## firstLock

``<firstLock>``标记的值为``false``或``true``。如果值为 ``true``，那么歌曲将不会被列在歌曲选择列表中，除非满足特定条件才能解锁歌曲。

## priority

``<firstLock>``标记的值为``false``或``true``。如果值为 ``true``，那么歌曲将不会被列在歌曲选择列表中，除非满足特定条件才能解锁歌曲。

## cueFileName

``<cueFileName>``标记包含一个库存数组，其``<id>``值等于在``root\app\data\AXXX\cueFile\cueFileXXXX``中找到的``CueFile.xml``文件中的 cueFile 的 ID。

## previewStartTime

``<previewStartTime>``标记包含一个整数，指定歌曲中预览开始的位置（以毫秒为单位），预览是歌曲在选曲屏幕上高亮显示时播放的部分。

## previewEndTime

``<previewEndTime>``标记包含一个整数，指定预览结束的歌曲位置（以毫秒为单位）。结束后，它将循环回到 ``<previewStartTime>`` 。

## worldsEndTagName

``<worldsEndTagName>``标记包含一个库存数组，其中``<id>``的值与乐曲的 WORLD'S END 类型相对应，``<str>``的值用汉字表示 WORLD'S END 类型的名称。如果音轨不是 WORLD'S END 音轨，则``<id>``的值为``-1``，``<str>``的值为``Invalid``。

## starDifType

``<starDifType>``标记包含一个未知整数。这个值可能与音乐的难度有关。

## stageName

``<stageName>`` 标记包含一个库存数组，其中的 ``<id>`` 值等于场景的 ID，即游戏过程中出现在栏位后面的背景视频，可在路径 ``root\app\data\AXXX\stage`` 中找到，而 ``<str>`` 值等于相应的 ``Stage.xml`` 文件中的 ``<name><str>`` 值。

## fumens

``<fumens>`` 的意思是 "谱面"，翻译过来就是 "音乐"，是包含每个难度的所有信息的标记。fumens 标记将包含 5 个 ``<MusicFumenData>`` 标记，每个难度一个，即使对应乐曲难度少于 5 个。

## MusicFumenData

``<MusicFumenData>``标记包含歌曲中每个难度的信息数组。下面列出的所有标记都是数组的一部分。

### resourceVersion

``<resourceVersion>`` 标记总是包含一个库存数组，其 ``<id>`` 值为 ``0`` 和一个空的 ``<str />`` 标记。

### type

``<type>``标记是一个库存数组，其中包含有关该特定``<MusicFumenData>``是哪种难度的信息。它有一个 ``<id>`` 值，可以是 ``0`` 到 ``4`` 之间的任意值。``<str>`` 值可以是 ``ID_00``、``ID_01``、``ID_O2``、``ID_03`` 或 ``ID_04``，但必须以与 ``<id>`` 标签值相同的数字结尾。``<data>`` 标记包含难度名称，可以是``BASIC``、``ADVANCED``、``EXPERT``、``MASTER``或``WORLD'S END``。该值必须依次与 ``<id>`` 和 ``<str>`` 标记相对应。例如，BASIC 的 ID 为 0，ADVANCED 的 ID 为 1，以此类推。

### enable

``<enable>``标记的值可以是``true``或``false``。如果值为``false``，难度将不会出现。在 WORLD'S END 的 ``<MusicFumenData>`` 标记上，如果歌曲是 normal，则此值设为 false，而在 WORLD'S END 曲目上，除了 WORLD'S END 之外的所有难度都设为 false。

### file

``<file>``标记包含一个``<path>``标记，该标记包含与特定难度相关联的 .c2s 文件的文件名。如果难度不存在且已禁用，则该标签将被空的 ``<path />`` 标签取代。

### level

``<level>``标记包含一个整数，等于游戏中显示的歌曲难度级别。如果难度不存在，或难度为 WORLD'S END，则标记的值为 ``0``。

### levelDecimal

``<levelDecimal>`` 标记包含一个 0-99 的整数，等于轨道的十进制难度。它与 ``<level>`` 标签相结合，可创建准确的难度级别。在游戏过程中看不到这个级别，而是用于按难度对曲目进行排序。如果难度不存在，或难度为 WORLD'S END，则标记的值为 ``0``。

### notesDesigner

``<notesDesigner>``标记总是空的，因此被写成``<notesDesigner />``。这是因为 ``.c2s`` 文件中包含了谱师的信息。

### defaultBpm

``<defaultBpm>``标记的值始终为``<0>``。
