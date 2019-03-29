---
title: 字体替换
description: 字体替换
ms.assetid: a67f42cd-1c10-46b7-8d24-0cb26339bc92
keywords:
- 打印机字体说明 WDK Unidrv，替换项
- 替换字体表 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bd35155aa40204511b834fc442a3cf79092cd64
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464303"
---
# <a name="font-substitution"></a>字体替换





对于提供驻留在硬件中的或盒字体的打印机，可以指定字体替换表。 通过提供字体替换表，您可以指定驻留在硬件中的或盒可以替换必须下载 TrueType 字体的字体。 当 Unidrv 接收在此类是 TrueType 字体中的文本时，它首先检查以查看字体替换表是否包含驻留在硬件中的替换字体。 如果 Unidrv 找到被替换的常驻字体和字体指标 （如字符集、 重量、 斜体、 方向和等等） 都兼容，使用常驻的字体。

您可以使用一系列创建默认字体替换表\*TTFS 条目。 每个条目的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* TTFS:<em>FontName</em> { *TTFontName:"<em>TTFontNameString</em>" *DevFontName:"<em>DeviceFontNameString</em>" <strong>}</strong></td>
</tr>
</tbody>
</table>

 

其中*FontName*是指定条目名称的符号*TTFontNameString*是标识要替换的 TrueType 字体的文本字符串和*DeviceFontNameString*是标识要使用的硬件驻留或盒字体的文本字符串。 下面是示例表：

```cpp
*TTFS: Arial
{
    *TTFontName: "Arial"
    *DevFontName "Arial"
}
*TTFS: TNR
{
    *TTFontName: "Times New Roman"
    *DevFontName: "Times New Roman"
}
*TTFS: CurrierNew 
{
    *TTFontName:  "Courier New"
    *DevFontName: "Courier New"
}
```

如果有重复\*TTFS 条目具有相同*FontName*值，由分析器读取的最后一个条目将取代上一个。

指定的替换表是默认的表，因为 Unidrv 允许用户修改替换项。

所有\*TTFS 条目必须位于 GPD 文件的根级别 (即，不在大括号内)。

若要控制是否启用字体替换默认情况下，使用\*TTFSEnabled？ 条目。 此条目的格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* TTFSEnabled？:<em>BooleanValue</em></p></td>
</tr>
</tbody>
</table>

 

其中*BooleanValue*是**TRUE**或**FALSE**。 如果*BooleanValue*是**TRUE**，Unidrv 使字体替换。 如果*BooleanValue*是**FALSE**，或如果不包括\*TTFSEnabled？ GPD 文件中的条目，直到用户启用 Unidrv 禁用字体替换。

\*TTFSEnable？ 条目是可重定位，但\*TTFS 项不是。 (有关可重定位的项的信息，请参阅什么到位置内\*开关，\*的情况下，和\*默认语句)。

### <a name="default-truetype-font-substitutions"></a>默认 TrueType 字体替换功能

名为 ttfsub.gpd 文件中提供了默认的表的 TrueType 字体替换功能。 若要使用它，添加以下条目 GPD 文件的根级别 (即，不在大括号内):

```cpp
*Include: "ttfsub.gpd"
```

此外，必须安装此文件。 有关详细信息，请参阅[打印机 INF 文件安装的部分](printer-inf-file-install-sections.md)。

 

 




