---
title: poolused
description: Poolused 扩展会根据用于每个池分配的标记显示内存使用摘要。
ms.assetid: e801342d-2536-43a3-992b-99942eb3c5ae
keywords:
- poolused Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolused
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef77fb5afa09c0669db9fa72ce8583453208897d
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025193"
---
# <a name="poolused"></a>!poolused


**! Poolused** extension 根据用于每个池分配的标记显示内存使用摘要。

```dbgcmd
!poolused [Flags [TagString]] 
```

## <a name="span-idddk__poolused_dbgspanspan-idddk__poolused_dbgspanparameters"></a><span id="ddk__poolused_dbg"></span><span id="DDK__POOLUSED_DBG"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的输出量和输出的排序方法。 这可以是以下位值的任意组合, 只不过不能将位 1 (0x2) 和 2 (0x4) 一起使用。 默认值为 0x0, 这会生成摘要信息, 按池标记排序。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示更详细的信息 (详细)。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
按非分页内存使用量排序显示。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
按分页内存使用量排序显示。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
(Windows Server 2003 及更高版本)显示会话池, 而不是标准池。

**请注意**  , 可以使用[ **!! session**](-session.md)命令在会话之间切换。

 

<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span>*TagString*   
指定池标记。 *TagString*是一个区分大小写的 ASCII 字符串。 星号 (\*) 可用于表示任意数量的字符; 问号 (？) 可以用来精确表示一个字符。 除非使用星号, 否则*TagString*的长度必须正好为四个字符。

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
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存池和池标记的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部机制*, 标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

**! Poolused**扩展从 Windows 的池标记功能收集数据。 在 Windows Server 2003 和更高版本的 Windows 上永久启用池标记。 在 Windows XP 和更早版本的 Windows 上, 必须使用[Gflags](gflags.md)启用池标记。

如果停止执行扩展, 则调试器会显示部分结果。

此命令的显示显示分页池和非分页池中每个标记的内存使用情况。 在这两种情况下, 显示屏都包含给定标记当前未完成的分配数以及这些分配所使用的字节数。

下面是此扩展的输出的部分示例:

```dbgcmd
0: kd> !poolused
   Sorting by  Tag

  Pool Used:
            NonPaged            Paged
 Tag    Allocs     Used    Allocs     Used
 1394        1      520         0        0UNKNOWN pooltag '1394', please update pooltag.txt
 1MEM        1     3368         0        0UNKNOWN pooltag '1MEM', please update pooltag.txt
 2MEM        1     3944         0        0UNKNOWN pooltag '2MEM', please update pooltag.txt
 3MEM        3      248         0        0UNKNOWN pooltag '3MEM', please update pooltag.txt
 8042        4     3944         0        0PS/2 kb and mouse , Binary: i8042prt.sys
 AGP         1      344         2      384UNKNOWN pooltag 'AGP ', please update pooltag.txt
 AcdN        2     1072         0        0TDI AcdObjectInfoG 
 AcpA        3      192         1      504ACPI Pooltags , Binary: acpi.sys
 AcpB        0        0         4      576ACPI Pooltags , Binary: acpi.sys
 AcpD       40    13280         0        0ACPI Pooltags , Binary: acpi.sys
 AcpF        6      240         0        0ACPI Pooltags , Binary: acpi.sys
 AcpM        0        0         1      128ACPI Pooltags , Binary: acpi.sys
 AcpO        4      208         0        0ACPI Pooltags , Binary: acpi.sys

...

 WmiG       30     6960         0        0Allocation of WMIGUID 
 WmiR       63     4032         0        0Wmi Registration info blocks 
 Wmip      146     3504       182    18600Wmi General purpose allocation 
 Wmit        1     4096         7    49480Wmi Trace 
 Wrpa        2      720         0        0WAN_ADAPTER_TAG 
 Wrpc        1       72         0        0WAN_CONN_TAG 
 Wrpi        1      120         0        0WAN_INTERFACE_TAG 
 Wrps        2      128         0        0WAN_STRING_TAG 
 aEoP        1      672         0        0UNKNOWN pooltag 'aEoP', please update pooltag.txt
 fEoP        1       16         0        0UNKNOWN pooltag 'fEoP', please update pooltag.txt
 hSVD        0        0         1       40Shared Heap Tag , Binary: mrxdav.sys
 hibr        0        0         1    24576UNKNOWN pooltag 'hibr', please update pooltag.txt
 iEoP        1       24         0        0UNKNOWN pooltag 'iEoP', please update pooltag.txt
 idle        2      208         0        0Power Manager idle handler 
 jEoP        1       24         0        0UNKNOWN pooltag 'jEoP', please update pooltag.txt
 mEoP        1       88         0        0UNKNOWN pooltag 'mEoP', please update pooltag.txt
 ohci        1      136         0        01394 OHCI host controller driver 
 rx..       3     1248         0        0UNKNOWN pooltag '  rx', please update pooltag.txt
 sidg        2       48         0        0GDI spooler events 
 thdd        0        0         1    20480DirectDraw/3D handle manager table 
 usbp       18    77056         2       96UNKNOWN pooltag 'usbp', please update pooltag.txt
 vPrt        0        0        18    68160UNKNOWN pooltag 'vPrt', please update pooltag.txt
 TOTAL     3570214 209120008     38769 13066104
```

 

 





