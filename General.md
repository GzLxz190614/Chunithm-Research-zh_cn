这是一份关于Chunithm的文件格式以及本研究文集的一般信息列表。其中包括感兴趣的文件列表、文件概览、其他文件链接（如有）以及本研究文件的元信息。

# Meta

* 本指南**并不保证**与当前版本的 Chunithm Paradise 同步。本指南是根据 "Chunithm Paradise"编写的。虽然我假定本指南中的几乎所有信息都将继续适用于 Chunithm 的后续版本，但我不能保证本指南与 Paradise Lost 和 Chunithm New 等后续版本100%兼容。此外，在新版中出现的 AIR SLIDE notes和 AIR CRUSH notes还没有谱面文档。未来可能会有所改变。
* 这**不是**在 Chunithm "clones"中创建自定义歌曲的指南。这包括像 SUSPlayer、Laverita 或 Seaurchin 等程序。这些游戏使用不同的谱面格式，并以完全不同的、通常是精简的方式实现自定义歌曲。
* Chunithm 经常使用``.xml``文件。为方便起见，本文档假定您了解``.xml``文件的基本格式。
* 提及 "音乐"和 "歌曲"时，指的是 ``music`` 文件夹中的文件，其中包括 ``Music.xml`` 和谱面文件。提到 ``audio`` 时，将指的是 ``cueFile`` 文件夹中的文件。
* 如果有人制作了一种工具来简化本文档中概述的任何流程，虽然显然不需要注明本文档的出处（查看 [UNLICENSE](UNLICENSE)）， 但我们仍将不胜感激。

# 歌曲如何结束

在 Chunithm 中游玩歌曲时，谱面将在最后一个 note 之后”结束"。这时，顶部的进度条动画和"FULL COMBO/ALL JUSTICE "图形就会出现。但是，歌曲会在音频文件播放完毕后"结束"。这时，歌曲结束时出现的任何技能（如支援技能）都会激活，不久后就会出现结算页面。

# MASTER 和 WORLD'S END 难度

除非满足两个条件之一，否则歌曲的 MASTER 难度将无法解锁：

* 玩家以 S 评级或更高评级通过了歌曲的MASTER难度，或

* 玩家使用的票卷允许游玩MASTER难度的谱面。(在票卷的 ``Ticket.xml`` 文件中的 ``<playMaster>`` 字段下注明已启用）。

在创建自制谱时，一定要注意这一点。如果谱面作者打算让其谱面具有MASTER难度，则应始终为MASTER难度提供有效的、可完成的谱面。否则，应将谱面设为其他 3 个正常难度之一。

除非玩家使用的票卷允许游玩 WORLD'S END 难度的乐曲，否则无法访问乐曲的 WORLD'S END 难度。(在票卷的``Ticket.xml``文件的``<playWorldsEnd>``字段下注明已启用） 创建自制谱时，不宜创建 WORLD'S END 谱面。除非玩家连接到 AIME 或 Minime 服务器，并购买或使用 WORLD'S END 票卷作弊，否则无法访问这些谱面。

# 文件夹

Chunithm 接收更新的方法是将新信息分别存储在 "root\app\data "中的 "AXXX "文件夹中。根据更新内容的不同，这些文件夹中的 "X "代表不同的数字。本文档中提到的 "AXXX "指的是未指定的 "A "文件夹。值得注意的是，虽然歌曲的补充文件（音频、封面、版权）通常都在同一个 ``A`` 文件夹中，但它们也有可能在其他文件夹中。目前，我们假设较新的 AXXX 文件夹将覆盖较旧的 AXXX 文件夹在游戏中的数据，尽管较旧的文件将保持不变，但这一点尚未得到证实。值得注意的是，Chunithm 的更新会定期删除某些预先存在的歌曲，通常是由于版权到期。此外，值得注意的是，Chunithm的主要更新会改变名称和增加新功能（例如，Amazon到Crystal，或Crystal到Paradise），不会涉及新的AXXX文件，而是将它们全部压缩到A000文件夹中。除其他二进制文件外，``root\app\bin``中的.exe也可能被覆盖。

# 文件类型

这是一份没有专门页面的相关文件类型的列表，以及这些文件的位置和必要的其他信息链接。这**并不是**一个广泛的列表，一些不感兴趣的文件将不包括在内。

## 音频文件

音乐音频文件位于``root\app\data\AXXX\cueFile\cueFileXXXXXX``中。插入点文件的 ID 可以在与相关歌曲的谱面文件位于同一文件夹中的 ``Music.xml`` 文件的 XML ``<cueFileName>`` 标记中找到。通常情况下，这些文件的 ID 与相应的音乐 ID 相同。这些文件以专有的[CRIWARE ADX2 音频格式](https://en.wikipedia.org/wiki/ADX_(file_format))编码，以``.awb``和``.acb``文件对形式存在。这些文件可由 [vgmstream](https://vgmstream.org/) 库，特别是 [foobar2000](https://www.foobar2000.org/) 的组件播放和转换。有关如何将自己的文件编码成这种格式的信息，请参阅 [Customs](https://github.com/Suprnova123/Chunithm-Research/blob/main/Customs.md) 文档。

## 封面文件

封面文件，也就是与歌曲相关联的图片，与谱面文件放在同一文件夹中，文件格式为 ``.dds``（DirectDraw Surface），可在 [GIMP](https://www.gimp.org/) 等软件中打开。插图文件的分辨率始终为 300x300。要模仿与 Chunithm 套装相同的文件大小，虽然通常没有必要，但可以从 GIMP 的导出设置中以 BC1 / DXT1 压缩导出任何自定义的 ``.dds`` 套装文件。

## 版权文件

版权文件是出现在特定歌曲选曲界面左下方的图像。由于文字后面的图像是独立的纹理，每个版权文件都会重复使用，因此版权文件应作为包含文字本身的文件使用。版权文件的格式始终是分辨率为 512x48 的``.dds``（DirectDraw Surface）文件格式，可以在``root\app\data\AXXX\rightsInfo\rightsInfoXXXXXX`` 中找到。要模仿与 Chunithm 权利文件相同的文件大小，虽然通常没有必要，但可以从 GIMP 的导出设置中使用 BC1 / DXT1 压缩导出任何自定义的 ``.dds`` 权利文件。

# Dummies

虚拟文件用于纹理，作为游戏希望纹理格式化的模板，主要是在分辨率方面。请注意，提供这些文件的 ``.png`` 版本只是为了方便，所有最终版本仍应使用 ``.dds`` 格式。

## Jacket Dummies

* [.dds](./_assets/jacket_dummy.dds)
* [.png](./_assets/jacket_dummy.png)

## Rights Dummies

* [.dds](./_assets/rights_dummy.dds)
* [.png](./_assets/rights_dummy.png)
