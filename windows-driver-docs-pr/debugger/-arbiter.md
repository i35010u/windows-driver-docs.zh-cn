---
title: 判
description: 仲裁器扩展显示当前的系统资源仲裁器和仲裁范围。
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
ms.openlocfilehash: 5c1310247f17da4ed8282d663b50340dc252e8b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800019"
---
# <a name="arbiter"></a>!arbiter


**！仲裁** 器扩展显示当前的系统资源仲裁器和仲裁范围。

```dbgcmd
    !arbiter [Flags] 
```

## <a name="span-idddk__arbiter_dbgspanspan-idddk__arbiter_dbgspanparameters"></a><span id="ddk__arbiter_dbg"></span><span id="DDK__ARBITER_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的仲裁器的类。 如果省略，则显示所有仲裁器。 可以自由合并这些位。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示 i/o 仲裁器。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示内存仲裁器。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示 IRQ 仲裁器。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示 DMA 仲裁器。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
显示总线编号仲裁器。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
不显示别名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。

<a name="remarks"></a>备注
-------

对于每个仲裁器， **！仲裁** 程序将显示系统资源的每个分配范围、一些可选标志、附加到该范围的 PDO (换言之，范围的所有者) ，以及此所有者 (（如果) 已知）的服务名称。

标志具有以下含义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>S</p></td>
<td align="left"><p>范围已共享</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>冲突范围</p></td>
</tr>
<tr class="odd">
<td align="left"><p>B</p></td>
<td align="left"><p>范围是启动分配的</p></td>
</tr>
<tr class="even">
<td align="left"><p>D</p></td>
<td align="left"><p>范围为驱动程序专用</p></td>
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

 

以下是示例：

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

在此示例中，"下一步" 行显示了资源范围 (由单独的 0x1A3) 、0x80E52778 的 PDO 和 i8042prt.sys 的服务组成。 此行上未列出任何标志。

你现在可以将 [**！ devobj**](-devobj.md) 与此 PDO 地址一起使用，查找设备扩展和设备节点地址：

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

 

 





