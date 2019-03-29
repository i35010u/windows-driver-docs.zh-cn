---
title: “驱动程序”
description: 在 Windows XP 和更高版本的 Windows 中，驱动程序扩展已过时。 而是使用 lm 命令。
ms.assetid: 48b69af3-bf00-43d3-ac1a-e9513ead8647
keywords:
- Windows 调试驱动程序
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- drivers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10b925d99cd29487ed4d3d1ce72a43861bf97213
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349212"
---
# <a name="drivers"></a>!drivers

在 Windows XP 和更高版本的 Windows， **！ 驱动程序**扩展已过时。 若要显示有关已加载的驱动程序和其他模块的信息，请使用[ **lm** ](lm--list-loaded-modules-.md)命令。 命令 lm t n 格式显示的信息非常类似于旧 **！ 驱动程序**扩展。 但是，此命令将不显示作为驱动程序的内存使用量 **！ 驱动程序**扩展未。 它将仅显示驱动程序的开始和结束地址、 映像名称和时间戳。 [ **！ Vm** ](-vm.md)并[ **！ memusage** ](-memusage.md)扩展可用于显示内存使用情况统计信息。

```dbgcmd
!drivers [Flags]
```

## <a name="span-idddkdriversdbgspanspan-idddkdriversdbgspanparameters"></a><span id="ddk__drivers_dbg"></span><span id="DDK__DRIVERS_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可以是下列值中的任意组合。 （默认值为 0x0。）

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括有关驻留和备用内存的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
如果设置此位，并且未设置位 2 (0x4)，显示将包含有关驻留、 待机、 和锁定的内存，以及加载程序条目地址信息。 如果设置位 2，这将导致显示被太多时间更长且更详细的列表的驱动程序映像。 有关头的信息是包括在内，按原样节的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示被太多时间更长且更详细的列表的驱动程序映像。 包含有关每个部分的信息。 如果设置位 1 (0x2)，这还将包括标头信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关驱动程序和其内存使用情况的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

下表给出了此命令显示的说明：

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
<td align="left"><p>设备驱动程序代码，以十六进制格式的起始地址。 如果导致停止的代码使用的内存地址介于之间驱动程序的基址和列表中的下一步驱动程序的基址，该驱动程序通常是错误的原因。 例如，Ncrc810.sys 的基础是 0x80654000。 它并 0x8065a000 之间的任何地址属于此驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>代码大小</p></td>
<td align="left"><p>大小，以千字节为单位，驱动程序代码，以十六进制和 decimal。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据大小</p></td>
<td align="left"><p>空间量，以千字节为单位，分配给数据，以十六进制和小数的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>已锁定</p></td>
<td align="left"><p>（仅当标志 0x2 使用）该驱动程序被锁定的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>驻留在</p></td>
<td align="left"><p>（仅当标志 0x1 或 0x2 使用）实际驻留在物理内存中的驱动程序的内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>备用服务器</p></td>
<td align="left"><p>（仅当标志 0x1 或 0x2 使用）处于备用状态的驱动程序的内存量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>加载程序项</p></td>
<td align="left"><p>（仅当标志 0x2 使用）加载程序条目地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>驱动程序名称</p></td>
<td align="left"><p>驱动程序文件名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>创建时间</p></td>
<td align="left"><p>链接的驱动程序日期。 请勿将此驱动程序，可以通过外部工具设置的文件日期。 驱动程序或可执行文件编译时，将由编译器设置链接日期。 它应该接近文件日期，但它并不总是相同。</p></td>
</tr>
</tbody>
</table>

 

下面是此命令的截断的示例：

```dbgcmd
kd> !drivers
Loaded System Driver Summary
Base     Code Size      Data Size      Driver Name  Creation Time
80080000 f76c0 (989 kb) 1f100 (124 kb) ntoskrnl.exe Fri May 26 15:13:00
80400000 d980  ( 54 kb) 4040  ( 16 kb) hal.dll      Tue May 16 16:50:34
80654000 3f00  ( 15 kb) 1060   ( 4 kb) ncrc810.sys  Fri May 05 20:07:04
8065a000 a460  ( 41 kb) 1e80   ( 7 kb) SCSIPORT.SYS Fri May 05 20:08:05
```

 

 





