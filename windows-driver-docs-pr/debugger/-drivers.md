---
title: “驱动程序”
description: 在 Windows XP 和更高版本的 Windows 中，驱动程序扩展已过时。 改为使用 lm 命令。
ms.assetid: 48b69af3-bf00-43d3-ac1a-e9513ead8647
keywords:
- 驱动程序 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- drivers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20701b8f00bda2228900a43d425fc422f99d69e1
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "70063902"
---
# <a name="drivers"></a>!drivers

>[!NOTE] 
> 在 Windows XP 和更高版本的 Windows 中， **！驱动程序**扩展已过时。 若要显示有关已加载的驱动程序和其他模块的信息，请使用[**lm**](lm--list-loaded-modules-.md)命令。 
>

命令 lm t n 以与旧 **！驱动程序**扩展非常相似的格式显示信息。 但是，此命令不会显示驱动程序的内存使用量，因为 **！驱动程序**扩展已完成。 它将仅显示驱动程序的开始和结束地址、映像名称和时间戳。 [ **！ Vm**](-vm.md)和[ **！ memusage**](-memusage.md)扩展可用于显示内存使用情况统计信息。

```dbgcmd
!drivers [Flags]
```

## <a name="span-idddk__drivers_dbgspanspan-idddk__drivers_dbgspanparameters"></a><span id="ddk__drivers_dbg"></span><span id="DDK__DRIVERS_DBG"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可以是以下值的任意组合。 （默认值为0x0。）

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位0（0x1）  
使显示内容包含有关驻留和备用内存的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位1（0x2）  
如果设置了此位并且未设置位2（0x4），则显示内容将包含有关驻留、备用和锁定内存以及加载程序条目地址的信息。 如果设置了 "位 2"，则会导致显示的驱动程序映像的更长、更详细的列表。 包含有关标头的信息，如节信息所述。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位2（0x4）  
使显示成为驱动程序映像的更长和更详细的列表。 包括有关每个部分的信息。 如果设置了位1（0x2），这还将包括标头信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅[即插即用调试](plug-and-play-debugging.md)此扩展命令的应用程序。 有关驱动程序及其内存使用情况的信息，请参阅 Windows 驱动程序工具包（WDK）文档和*Microsoft Windows 内部*内容，标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

下表给出了此命令的显示说明：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Base</p></td>
<td align="left"><p>设备驱动程序代码的起始地址，以十六进制表示。 当导致停止的代码所使用的内存地址与列表中下一个驱动程序的基址之间时，该驱动程序通常是导致错误的原因。 例如，Ncrc810 的基础为0x80654000。 该和0x8065a000 之间的任何地址都属于此驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>代码大小</p></td>
<td align="left"><p>驱动程序代码的大小（以 kb 为单位），采用十六进制和十进制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据大小</p></td>
<td align="left"><p>为数据的驱动程序分配的空间量（以 kb 为单位），采用十六进制和十进制。</p></td>
</tr>
<tr class="even">
<td align="left"><p>已锁定</p></td>
<td align="left"><p>（仅当使用标志0x2 时）驱动程序锁定的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>常驻</p></td>
<td align="left"><p>（仅当使用标志0x1 或0x2 时）实际驻留在物理内存中的驱动程序内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>转入</p></td>
<td align="left"><p>（仅当使用标志0x1 或0x2 时）处于待机状态的驱动程序的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>加载器条目</p></td>
<td align="left"><p>（仅当使用标志0x2 时）加载器条目地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序名称</p></td>
<td align="left"><p>驱动程序文件名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建时间</p></td>
<td align="left"><p>驱动程序的链接日期。 不要将其与驱动程序的文件日期混淆，可以通过外部工具进行设置。 当编译驱动程序或可执行文件时，编译器将设置链接日期。 它应该接近文件日期，但并不总是相同。</p></td>
</tr>
</tbody>
</table>

 

下面是此命令的一个截断示例：

```dbgcmd
kd> !drivers
Loaded System Driver Summary
Base     Code Size      Data Size      Driver Name  Creation Time
80080000 f76c0 (989 kb) 1f100 (124 kb) ntoskrnl.exe Fri May 26 15:13:00
80400000 d980  ( 54 kb) 4040  ( 16 kb) hal.dll      Tue May 16 16:50:34
80654000 3f00  ( 15 kb) 1060   ( 4 kb) ncrc810.sys  Fri May 05 20:07:04
8065a000 a460  ( 41 kb) 1e80   ( 7 kb) SCSIPORT.SYS Fri May 05 20:08:05
```

 

 





