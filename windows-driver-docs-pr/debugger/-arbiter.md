---
title: 仲裁器
description: 仲裁器扩展显示当前的系统资源仲裁器，并仲裁范围。
ms.assetid: 95149538-6fcd-4638-b35f-4e1a562e5231
keywords:
- 仲裁器 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- arbiter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2b46e2b87090e5096ca131515dd02cf86bab3e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564654"
---
# <a name="arbiter"></a>!arbiter


**！ 仲裁器**扩展显示当前的系统资源仲裁器和仲裁的范围。

```dbgcmd
    !arbiter [Flags] 
```

## <a name="span-idddkarbiterdbgspanspan-idddkarbiterdbgspanparameters"></a><span id="ddk__arbiter_dbg"></span><span id="DDK__ARBITER_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定显示哪些类仲裁器。 如果省略，将显示所有仲裁器。 可以自由地组合这些位。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示 I/O 仲裁器。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示内存仲裁器。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示 IRQ 仲裁器。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示 DMA 仲裁器。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
显示总线数字仲裁器。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)  
不会显示别名。

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

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。

<a name="remarks"></a>备注
-------

对于每个仲裁器， **！ 仲裁器**显示每个分配范围的系统资源，某些可选标志，PDO 附加到该范围 （即，该范围的所有者），并且此所有者的服务名称 （如果已知）。

标志的含义如下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>共享范围</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>范围发生冲突</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B</p></td>
<td align="left"><p>范围是启动分配</p></td>
</tr>
<tr class="even">
<td align="left"><p>D</p></td>
<td align="left"><p>范围是独占的驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>A</p></td>
<td align="left"><p>范围别名</p></td>
</tr>
<tr class="even">
<td align="left"><p>P</p></td>
<td align="left"><p>范围正解码</p></td>
</tr>
</tbody>
</table>

 

下面是一个示例：

```console
kd> !arbiter 4

DEVNODE 80e203b8 (HTREE\ROOT\0)
  Interrupt Arbiter "" at 80167140
    Allocated ranges:
      0000000000000000 - 0000000000000000   B   80e1d3d8 
      0000000000000001 - 0000000000000001   B   80e1d3d8 
 .....
      00000000000001a2 - 00000000000001a2    
        00000000000001a2 - 00000000000001a2  CB   80e1d3d8 
        00000000000001a2 - 00000000000001a2  CB   80e52538  (Serial)
      00000000000001a3 - 00000000000001a3       80e52778  (i8042prt)
      00000000000001b3 - 00000000000001b3       80e1b618  (i8042prt)
 Possible allocation:
      < none >
```

在此示例中下, 一步至最后一线显示的资源范围 （其中包括 0x1A3 单独），0x80E52778，对 PDO 和 i8042prt.sys 服务。 这一行不列出了任何标志。

现在，您可以使用[ **！ devobj** ](-devobj.md)与此 PDO 地址来查找扩展和设备节点地址的设备：

```console
kd> !devobj 80e52778
Device object (80e52778) is for:
 00000034 \Driver\PnpManager DriverObject 80e20610
Current Irp 00000000 RefCount 1 Type 00000004 Flags 00001040
DevExt 80e52830 DevObjExt 80e52838 DevNode 80e52628 
ExtensionFlags (0000000000)  
AttachedDevice (Upper) 80d78b28 \Driver\i8042prt
Device queue is not busy.
```

 

 





