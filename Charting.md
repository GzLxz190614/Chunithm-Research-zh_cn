这是关于游戏中使用的谱面文件的基本文档。这些文件显示了歌曲的结构，如 note 位置和节奏。

# 须知事项

* 本文档不保证 100%准确。某些 tag 定义基于假设，可能需要进一步测试。
* 该文件格式中的大多数计数都从 0 开始。小节为 0 表示歌曲开始，单元格为 0 表示左边的第一个单元格，等等。
* 谱面文件的位置在 ``root\app\data\AXXX\music\musicXXXX`` 中。谱面的文件格式为``.c2s``，是纯文本文件，可以用 Notepad++ 等工具打开。
* 一个单元格是游戏画面上 note 的对应键。游戏区有 16 列，从左到右的数字为 0-15。
* 小节是包含特定节拍的时间函数。每个小节通常包含 4 个节拍，并在整首歌曲中保持相对一致。
* 根据我的经验，除非注释的格式非常特殊，否则 Chunithm 通常会忽略注释。在现有的谱面文件中，使用制表符而不是空格来为注释添加修饰符是有效的，而使用空格则无效。根据我的经验，这是 Notepad++ 独有的功能。
* Chunithm 会在选择时重新加载``.c2s``文件。这意味着只需重新选择正在更改的歌曲，就可以调试自定义谱面。为了简化这一过程，请使用 "DANGER "技能，如 "今わの際"（技能 ID 102005），并在自定义音符后的几小节中放置 ≈20 TAP 音符。这样，您就会自动使 Track 失败，并能更快地重新选择 Track，而无需等待歌曲结束。

# Tags

## VERSION

通常设置为 1.08.00。（表示用于谱面设计的 ``.c2s`` 处理程序的版本？）

## MUSIC

通常设置为 0。在 ``Music.xml`` 文件包含该 ID 之前，它可能是音乐的 ID。

## SEQUENCEID

通常设置为 0。

## DIFFICULT

通常设置为 00。在 ``Music.xml`` 文件包含它之前，它可能是音乐的难度（BASIC, ADVANCED, EXPERT, MASTER, WORLD'S END）。

## LEVEL

通常设置为 0.0。在 ``Music.xml`` 包含谱面文件之前，它可能是谱面文件的级别。

## CREATOR

指定谱面文件的谱师。请注意，除非难度设置为 "BASIC" 或 "ADVANCED" ，否则该字符串将出现在选曲界面歌曲卡片的左下方。

## BPM_DEF

指定默认 BPM。

### 示例:

| 1 | 2 | 3 | 4 |
| ---- | ---- | ---- | ---- |

1 通常包含真正的默认 BPM，或歌曲开始时的 BPM。2 通常包含备选 BPM，或歌曲除 1 中的 BPM 之外最常用的 BPM。3 和 4 似乎分别反映了 2 和 1。

## RESOLUTION

表示歌曲的分辨率。始终设置为 384。

## CLK_DEF

始终设置为 384。

## PROGJUDGE_BPM

始终设置为 240.000。

## PROGJUDGE_AER

始终设置为 0.999。

## TUTORIAL

指定谱面是否为教程谱面。

## BPM

指定歌曲中指定小节的 BPM。

### 示例:

| Beginning Measure | Offset | BPM |
| ---- | ---- | ---- |

## MET

指定歌曲中指定小节的时间标记。

### 示例:

| Beginning Measure | Offset | Second Value | First Value |
| ---- | ---- | ---- | ---- |

需要注意的是，时间符号的数值是相反的。值得一提的是，这纯粹是表面现象。该值唯一会影响的是游戏画面上细长小节线的位置。

## SFL

指定歌曲指定小节时的播放速度。

### 示例:

| Beginning Measure | Offset | Duration | Multiplier |
| ---- | ---- | ---- | ---- |

值得注意的是，乘数的精确度必须为 0.000001，即小数点后必须有六位数。该值将乘以玩家当前的游戏速度，因此音符会根据该值显示得更快或更慢。该值纯粹是外观上的，不会影响 .c2s 文件中音符的位置，只有播放器会看到区别。该值也可以设为负数，这将导致谱面反向移动，通常用于美观目的，如[Fracture Ray 的 MASTER 谱面的这一部分](https://youtu.be/5m7bMyIDoec?t=48)。

# Notes

## 通用 Note 示例

| Note Type | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

### Note 类型

note 类型是指您希望在此特定点上放置的 note 类型。有多种类型的 note 可以使用，其中大部分都有附加变量，这些变量将附加到典型模式的末尾。稍后会有更多信息解释这些 note 。

#### Note 类型:

* TAP (tap)
* CHR (ex-note)
* HLD (hold)
* SLD (slide)
* SLC (slide control point)
* FLK (flick)
* AIR (air)
* AUR (air up-right)
* AUL (air up-left)
* AHD (air hold)
* ADW (air downwards)
* ADR (air down-right)
* ADL (air down-left)
* MNE (mine)

### Measure

小节是您希望音符所在的具体小节。每个小节（通常）为 4 拍。该值从 0 开始无限延续，但应始终与歌曲一起结束。

### Offset

时间函数，用于显示音符或定时点与小节的偏移量。这取决于歌曲的分辨率，由 RESOLUTION（分辨率）tag 指定。全分辨率为一小节，因此分辨率为 384 时，小节的第一拍为 0，第二拍为 96，第三拍为 192，第四拍为 288。要获得所需的节拍，先将分辨率除以 4，再乘以所需的节拍，然后减去分辨率除以 4。

如果是几分之一拍，先用分辨率除以 4，再乘以所需的几分之一拍。然后将结果与所需节拍相加。

The function for this would be:

```b(r/4)-(r/4) + f(r/4)```

其中，b 是四舍五入为整数的所需节拍，r 是歌曲的分辨率，f 是节拍的分数。

例如，如果我想在一首分辨率为 384 的四拍子歌曲的第 2 个1/2 拍出现一个 note ，我会执行以下步骤：

```
2(384/4)-(384/4) + 1/2(384/4)
192 - 96 + 48
144
```

### Cell

如上所述，单元格是音符应出现在游戏栏中的数字 ID。请注意，该值应是音符从**左侧**首先出现的列。

### Width

宽度（Width）值与单元格值不同，它表示音符的宽度，从单元格中列出的值向右延伸。最小值为 1，这意味着 note 只占用单元格中列出的列。例如，如果单元格值为 7 的 note 宽度为 3，则该 note 将占用第 7、8 和 9 列。

## Additional Note Values

大多数备注类型需要附加信息才能正常运行。本节将举例说明附注使用的模式，然后解释未包含在通用模式中的任何值。任何带引号的值都表示与该附注一致的值。

### Tap

Tap 是最基本的可以放在谱面的 note 。它们只要求玩家在规定的时间内敲击 note 所在的单元格。

#### 示例:

| "TAP" | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

Tap notes 与上述通用示例没有区别。

### Ex-Notes

Ex-Notes 与 Tap 类似，但玩家只要准确敲击，就能获得更多分数。

#### 示例:

| "CHR" | Measure | Offset | Cell | Width | Unknown |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Unknown： 数值似乎总是 "UP"、"CE "或 "DW"。（译者注：打击Ex-Notes后的动画移动方向？）

### Hold

Hold 与 Tap 类似，但要求玩家连续按住指定单元格一段时间。

#### 示例: 

| "CHR" | Measure | Offset | Cell | Width | Duration |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Duration：音符需要按住的时间。该值与偏移量的格式相同。

### Slide

Slide 与 Hold 类似，但可以在保持的同时在单元格之间移动。Slide 有两种类型：SLD 和 SLC。以直线开始的 Slide 以 SLD 开始，而立即开始移动的 Slide 则以 SLC 开始。所有 Slide 都以 SLD note 结束。

#### 示例:

| "SLD"/"SLC" | Measure | Offset | Cell | Width | Duration | End Cell | End Width |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

* Duration：note 移动到目标单元格所需的时间。该值与偏移量的格式相同。
* End Cell：Slide 在持续时间内移动的列。与单元格值类似，该值将位于单元格左侧，范围在 0-15 之间。要使 Slide 在持续时间内保持直线，可将单元格结束值设置为与单元格值相同。
* End Width：Slide 在持续时间结束时的宽度。与 "宽度 "值类似，该值可在 1-16 之间任意设置。如果 "结束宽度 "与 "原始宽度 "不同，Slider 的宽度将在 Slide 播放过程中逐渐缩小或扩大。

在您调用同一单元格中的 SLD 之前，Slide 不会结束，而此时另一个 Slide 也在同一单元格中，之后不会出现另一个 Slide 。在连续 Slide 中间调用 SLD 会在该特定点添加一个额外的蓝色 note ，这纯粹是为了美观（译者注：？）。要调整 Slide 而不添加其他音符，请使用 SLC。

Slide 左右快速晃动的功能并不是游戏的内置功能，而只是让 Slide 在很短的偏移时间内左右移动几个单元格。

### Flick

Flick 需要玩家将手指放在flick note  所在的单元格内，然后向任意水平方向轻滑。

#### 示例:

| "FLK" | Measure | Offset | Cell | Width | Unknown |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Unknown：值始终为 "L"。请注意，这不是华东的方向，Flick 可以从任何方向滑动。(译者注：不会是SEGA把定向滑动删了吧））

### Air

Air 是指玩家通过物理键盘上方的红外传感器举起双手。与其他 note 不同，这些 note 是对已有 note 的修改。这种 note 也有不同的外观版本，但功能完全相同。

#### 示例:

| "AIR"/"AUR"/"AUL" | Measure | Offset | Cell | Width | Target Note |
| ---- | ---- | ---- | ---- | ---- | ---- |

* AIR/AUR/AUL：这些 note 类型在功能上完全相同，但会影响 note 上方箭头的外观。AIR 有一个向上的箭头，AUR 有一个向上向右的箭头，而 AUL 则有一个向上向左的箭头。
* Target Note：该值指定了 Air note 所 "吸附 "的 note 。该 note 应与 Air Note 位于同一单元、小节和偏移量中。此外，建议只在 note 的末尾使用该 note ，而不是在延音的中间使用。对于高级谱面，可以放弃这一建议。

## Air Hold

Air Hold 是指玩家在完成 Air Note 后，将双手举向传感器。Air Hold总是会自动以一个空中向下的 note 结束。（译者注：NEW!! 后好像可以不需要末尾有向下动手的 note）

#### 示例:

| "AHD" | Measure | Offset | Cell | Width | Target Note | Duration |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |

* Target Note：该值指定了 Air note 所 "吸附 "的 note 。该 note 应与 Air note 位于同一单元、小节和偏移量中。此外，建议只在 note 的末尾使用该 note ，而不是在延音的中间使用。对于高级谱面，可以放弃这一建议。
* Duration: note 移动到目标单元格所需的时间。该值与偏移量的格式相同。

要在持续的 air note 中加入 mid-air downwards notes ，可将第一个 air hold note 持续到 mid-air note 的位置，然后再加入一个 air hold note ，其起始位置与前一个 air hold note 的结束位置偏移相同。

### Downwards

Downwards 是指玩家通过物理键盘上方的红外传感器将手放下。与其他 note 不同，这些note 是对已有note 的修改。note 也有不同的外观版本，但功能完全相同。

#### 示例:

| "ADW"/"ADR"/"ADL" | Measure | Offset | Cell | Width | Target Note |
| ---- | ---- | ---- | ---- | ---- | ---- |

* ADW/ADR/ADL：每种 note 类型的功能都是相同的，只是会影响 note 上方箭头的外观。ADW 箭头向下，ADR 箭头向右，ADL 箭头向左。
* Target Note：该值指定了 downwards note "吸附 "的 note。该 note 应与 downwards note 位于同一单元、小节和偏移量中。此外，建议只在 note 的末尾使用该 note，而不是在延音的中间使用。对于高级谱面，这一建议可不予考虑。

### Mines

Mine 要求玩家不要触碰放置 mine 的单元格。触碰 note 将导致玩家失分，并可能导致Track Lost(卡车丢失）)。

| "MNE" | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

Mine 所需的信息与 Tap 相同，只需遵循上述通用模式即可。

# Notes 演示

下面是 Cyaegha 的 MASTER 难度谱面，分辨率（RESOLUTION）为 386。

```
TAP	8	0	6	4
TAP	8	0	12	4
SLC	8	96	4	4	7	3	4
TAP	8	96	10	4
SLC	8	103	3	4	10	2	4
SLC	8	113	2	4	13	1	4
SLC	8	126	1	4	22	0	4
SLD	8	148	0	4	236	0	4
TAP	8	192	8	4
SLC	8	288	6	4	4	7	4
SLC	8	292	7	4	12	9	4
SLC	8	304	9	4	9	10	4
SLC	8	313	10	4	12	11	4
SLC	8	325	11	4	23	12	4
SLD	8	348	12	4	36	12	4
AHD	9	0	0	4	SLD	192
CHR	9	0	4	8	CE
AIR	9	0	4	8	CHR
AHD	9	0	12	4	SLD	192
TAP	9	288	3	4
TAP	9	288	9	4
```

以下是本节的游戏玩法。我们将对上述节选的每一行进行细分，以查看其相应的游戏模式。

![Demonstration of Cyaegha Excerpt](./_assets/cyaegha%20example.gif)

开头的两个 Tap 显示为：
```
TAP	8	0	6	4
TAP	8	0	12	4
```

这些行中数值的顺序如下：

``Tap note | on the 8th measure | with an offset of 0 | starts on cell 6/cell 12 | extends 4 cells to the right``

可以看出，这些 note 应该是同时出现的，因为它们具有相同的小节和偏移量。请记住，这些单元格的标记是 0-15，也就是说左边的第一个单元格是 0 单元格。

接下来的两个 note 是同时出现的 slide 和 tap。在文件中显示为：
```
SLC	8	96	4	4	7	3	4
TAP	8	96	10	4
```

请注意，slide 的 note 类型是 SLC，因为 slide 是在滑动中开始的。如果 slide 一开始是静止的，它的 note 类型就会是 SLD。

Slide note 的数值顺序如下：

``Slide note | on the 8th measure | with an offset of 96 | starts on cell 4 | extends 4 cells to the right | has a duration of 7 resolution | ends on cell 3 | ends with a width of 4``

这里有几件重要的事情需要注意。首先，小节数为 8，偏移量为 96，这意味着 note 发生在第 8 小节的第二拍（记住，偏移量为 0 意味着第一拍）。它的持续时间也很短，只有 7 分辨率。这意味着 slide 的持续时间几乎只有小节的 2/100。之所以这么短，是因为它的设计看起来像一条曲线。后来有一些 SLC note 附着在第一个 slide 上，逐渐将形状变为曲线。

稍后的 tap 的数值顺序为

``Tap note | on the 8th measure | with an offset of 96 | starts on cell 10 | extends 4 cells to the right``

同样，由于这两个 note 出现在相同的小节和偏移量上，因此它们是同时发生的。

接下来的说明是 slide 的几个控制点，以及创建一个新 slide 和一个 tap 说明。它们分别是
```
SLC	8	103	3	4	10	2	4
SLC	8	113	2	4	13	1	4
SLC	8	126	1	4	22	0	4
SLD	8	148	0	4	236	0	4
TAP	8	192	8	4
SLC	8	288	6	4	4	7	4
SLC	8	292	7	4	12	9	4
SLC	8	304	9	4	9	10	4
SLC	8	313	10	4	12	11	4
SLC	8	325	11	4	23	12	4
SLD	8	348	12	4	36	12	4
```

这里有几件重要的事情需要注意。首先，顶部的 SLC 相继出现的速度非常快。如上所述，这是因为要创建一个弯曲的 slide ，所以要非常精确才能看起来流畅。紧随其后的还有一个 SLD，其持续时间为 236 分辨率。这一点很重要，因为你可以看到这个 slide 应该与另一个 slide 同时结束。如果将偏移量（148）和持续时间相加，就会得到 384 的值。如果将底部第二个 SLD 的偏移量和持续时间相加，结果也是 384。由于它们都在同一量程上，这表明它们将在彼此相同的时间结束。值得一提的是，第二对 SLC 与第一对 SLC 无关。它们从另一个 slide 的独立单元格开始，因此它创建了一个新的slde ，而不是扩展之前的 slide 。

选段的最后部分包含几个 air note 、一个 air hold, 、一个 ex-note 和几个 tap 。这些 note 在文件中显示为：
```
AHD	9	0	0	4	SLD	192
CHR	9	0	4	8	CE
AIR	9	0	4	8	CHR
AHD	9	0	12	4	SLD	192
TAP	9	288	3	4
TAP	9	288	9	4
```

您会注意到，AHD、AIR 和 CHR note 都是同时开始的，因为它们共享相同的小节和偏移量。让我们来分解每个 note 。

AHD 的说明如下：

``Air hold note | on the 9th measure | with an offset of 0 | starts on the 0th cell/12th cell | extends to the right by 4 cells | leaches off of the Slider note that occupies that same cell | has a duration of 192 resolution``

CHR 的说明如下：

``Ex-note | on the 9th measure | with an offset of 0 | starts on the 4th cell | extends to the right by 8 cells | CE modifier``

AIR note 的说明如下：

``Air note | on the 9th measure | with an offset of 0 | starts on the 4th cell | extends to the right by 8 cells | leaches off of the ex-note that occupies the same cell``

节选最后以两个 TAP note 结束，其含义如下：

``Tap note | on the 9th measure | with an offset of 288 | starts on the 3rd/9th cell | extends to the right by 4 cells``

对 Cyaegha 节选的分析到此结束。

# 结束 Tags

**注意：** 这些值虽然是经过最少的测试得出的，但似乎不会影响 track 的功能。因此，在创建自定义 track 时，可以完全忽略这些值。

## T_REC_XXX

``XXX`` 被替换为 note 类型（TAP、CHR、FLK、MNE、HLD、SLD、AIR、AHD）的简称，以及一个标有 ``T_REC_ALL``的字段。它似乎是对每个谱面中指定类型 note 数量的计数。``T_REC_ALL``等于前面的 ``T_REC_XXX ``字段的值相加。

## T_NOTE_XXX

似乎与 ``T_REC_XXX`` 相同，但尽管在同一个谱面中，数值却彼此不同。

## T_NUM_XXX

似乎与 ``T_REC_XXX`` 和 ``T_NOTE_XXX`` 相同，但没有 ``T_XXX_ALL`` 字段，取而代之的是一个未知的 ``T_NUM_AAC`` 字段。

## T_CHRTYPE_XX

``XX`` 被替换为 CHR note 修饰符（UP、DW、CE）的缩写。该命令用于计算音轨中带有指定修饰符的 CHR note 的数量。

## T_LEN_XXX

``XXX`` 被替换为 "sustain" notes(持续音符)（HLD、SLD、AHD、ALL）的简称，以及一个标有 ``T_LEN_ALL`` 的字段。该字段似乎与 ``T_REC_XXX`` 相同，但它计算的是指定类型的 "sustain" notes(持续音符) 的有效毫秒数。``T_LEN_ALL`` 等于前面的 ``T_LEN_XXX`` 字段的值相加。

## T_JUDGE_XXX

U未知。

## T_FIRST_XXXX

有两个tag：``T_FIRST_MSEC`` 和``T_FIRST_RES``。两者分别表示第一个 note 的时间戳（毫秒）和分辨率。

## T_FINAL_XXXX

有两个tag：``T_FINAL_MSEC`` 和``T_FINAL_RES``。这两个标记分别表示最后一个 note 的时间戳（毫秒）和分辨率。这不一定等于谱面文件中列出的 note 的时间戳，因为 sustained notes(持续音符)会将时间戳移动到音符结束时。

## T_PROG_XX

有 20 个tag，从 ``T_PROG_00`` 开始，以 5 个为增量递增到 ``T_PROG_95`` 作为最终标记。未知。

# Cosmetics

本文档的这一部分将概述游戏中发现的 note 的各种外观信息。这不是关于 note 的通用信息，例如 note 的具体颜色，而是在创建自定义谱面时可能有用的小细节。这些信息不会对游戏产生任何影响。

## Flick Notes

Flick Notes 显示为一个灰色 note ，内含一个蓝色小 note 。蓝色 note的宽度是 tap 的三分之一，位于 note 的中心。

## Air/Down Notes

Air note 和 down note 的上方或下方都有一个箭头，其宽度与相关 note 相同。这些 note 的角度总是指向原 note左侧或右侧的单元格。