---
title: 生成已跳过的宏块
description: 生成已跳过的宏块
ms.assetid: 98ea004b-347d-4299-a23c-da0a9d0e844f
keywords:
- 宏块 WDK DirectX va，因此已跳过块效应
- 跳过块效应 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28852808309a5fbda66c7f7d546b710ebe033601
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391252"
---
# <a name="generating-skipped-macroblocks"></a>生成已跳过的宏块


## <span id="ddk_generating_skipped_macroblocks_gg"></span><span id="DDK_GENERATING_SKIPPED_MACROBLOCKS_GG"></span>


在 DirectX VA 已跳过宏块生成不同一定程度上的 mpeg-2 视频部分第 7.6.6。 在 DirectX VA 已跳过宏块在一个单独的宏块管理命令，而不是从上述 nonskipped 宏块的类型推断中生成和显示 （例如，MPEG 2，生成跳过的方法中的图片类型宏块取决于是否图片*P 图片*或*B 图片*。)

时生成和使用已跳过块效应，所需满足以下条件：

- 已跳过宏块有没有剩余的差异。

- 可以重复使用递增的宏块控制命令操作生成已跳过块效应**wMBaddress**。 (每个后续的已跳过宏块生成第一个相同的方式除外的递增的值**wMBaddress**。)

- 正在跳过宏块仅限于包装从图中的宏块的新行。 （单独宏块控制命令必须发送生成块效应的每一行的第一个宏块。）

- 具有一个非零值的宏块控制命令的内容*MBskipsFollowing*等效 (除外的值*MBskipsFollowing*) 的显式规范的第一个内容在本系列的已跳过块效应。 因此，每当*MBskipsFollowing*零，以下结构成员和变量必须全部为等于零不是：*Motion4MV、 IntraMacroblock，* **wPatternCode**<em>，并</em>**全球合作伙伴大会\_Overflow**。

由于前三个上述条件，加速器可能实现运动补偿 (当*Motion4MV*为零) 通过将指定的动作矢量应用于矩形的宽度等于中的下列表达式组件，并向色度组件中同样指定矩形的亮度。 按快捷键而不是通过使用可执行此矩形区域运动补偿方法*MBskipsFollowing*+ 1 重复同一宏块控制操作。

```cpp
(bMacroblockWidthMinus1+1) X (MBskipsFollowing+1)
```

**BMacroblockWidthMinus1**中包含成员[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)。 *MBskipsFollowing*变量处于**wMBtype**的每个宏块控制结构的成员。

### <a name="span-idskippedmacroblocksinh263annexfspanspan-idskippedmacroblocksinh263annexfspanspan-idskippedmacroblocksinh263annexfspanskipped-macroblocks-in-h263-annex-f"></a><span id="Skipped_Macroblocks_in_H.263__Annex_F_"></span><span id="skipped_macroblocks_in_h.263__annex_f_"></span><span id="SKIPPED_MACROBLOCKS_IN_H.263__ANNEX_F_"></span>已跳过宏块中 H.263 （附录 F）

使用高级的预测模式 active (附录 F)，已跳过 H.263 中的块效应的生成要求 nonskipped 块效应 DirectX VA 宏块控制命令中作为表示某些已跳过块效应。 这样做是为了生成*OBMC*这些宏块中的效果。

### <a name="span-idgeneratingskippedmacroblocksinmpeg-2examplespanspan-idgeneratingskippedmacroblocksinmpeg-2examplespanspan-idgeneratingskippedmacroblocksinmpeg-2examplespangenerating-skipped-macroblocks-in-mpeg-2-example"></a><span id="Generating_Skipped_Macroblocks_in_MPEG-2_Example"></span><span id="generating_skipped_macroblocks_in_mpeg-2_example"></span><span id="GENERATING_SKIPPED_MACROBLOCKS_IN_MPEG-2_EXAMPLE"></span>MPEG 2 的示例中生成已跳过块效应

下面的示例演示如何生成已跳过宏块时使用宏块控制命令。 出于演示目的，假设在 MPEG 2 位流，七个宏块按以下方式使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块数量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>编码的残留差别，</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>编码的残留差别，</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>编码的残留差别，</p></td>
</tr>
</tbody>
</table>

 

（至少） 以下七个宏块需要生成的表所示的五个 DirectX VA 宏块控制命令。 *MBskipsFollowing*变量指示已跳过宏块的数目。 **WMBaddress**成员指示宏块的地址。 *MBskipsFollowing*并**wMBaddress**中包含[ **DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)，并[ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563993)结构。 ( *MBskipsFollowing*中定义变量**dwMB\_SNL**结构成员。)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块命令</th>
<th align="left">成员值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>第一个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 0</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>第二个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 1</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第三个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 2</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>第四个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 3</p>
<p><em>MBskipsFollowing</em> = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第五个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 6</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
</tbody>
</table>

 

 

 





