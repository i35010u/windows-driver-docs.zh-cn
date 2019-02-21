---
title: poolused
description: Poolused 扩展显示基于标记用于每个池分配的内存使用汇总。
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
ms.openlocfilehash: 52af1d34c077699dc9401fb163a0008f8c947be9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540987"
---
# <a name="poolused"></a>！ poolused


**！ Poolused**扩展显示基于标记用于每个池分配的内存使用汇总。

```dbgcmd
!poolused [Flags [TagString]] 
```

## <a name="span-idddkpooluseddbgspanspan-idddkpooluseddbgspanparameters"></a><span id="ddk__poolused_dbg"></span><span id="DDK__POOLUSED_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示的输出量和排序输出的方法。 这可以是以下位值的任意组合，只不过位 1 (0x2) 和 2 (0x4) 不能一起使用。 默认值为 0x0，生成按池标记的摘要信息。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示更详细的详细信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
使用排序的非分页内存量的显示。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
对显示排序的分页的内存使用。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
(Windows Server 2003 及更高版本)显示会话池而不是标准的池。

**请注意**  可以使用[ **！ 会话**](-session.md)命令会话之间切换。

 

<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span> *TagString*   
指定的池标记。 *TagString*是区分大小写的 ASCII 字符串。 星号 (\*) 可以用于表示任意数量的字符; 问号 （？） 可以用于表示一个字符。 除非使用一个星号，否则*TagString*必须是长度为四个字符。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

内存池和池标记有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

**！ Poolused**扩展从标记的 Windows 功能的池中收集数据。 Windows Server 2003 和更高版本的 Windows 上永久启用池标记。 在 Windows XP 和 Windows 的早期版本中，必须启用池通过使用标记[Gflags](gflags.md)。

如果停止执行扩展，在完成之前，调试器将显示部分结果。

此命令显示在页面缓冲的池和非分页缓冲的池显示为每个标记的内存使用。 在这两种情况下，显示内容包括有关给定标记当前未释放分配数和使用的那些分配量的字节数。

下面是输出的此扩展中的一个部分示例：

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

 

 





