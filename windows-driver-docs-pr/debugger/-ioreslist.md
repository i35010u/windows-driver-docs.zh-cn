---
title: ioreslist
description: Ioreslist 扩展显示 IO_RESOURCE_REQUIREMENTS_LIST 结构。
ms.assetid: cb599656-2e0a-41ec-8358-a42047974dea
keywords:
- ioreslist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ioreslist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69a92e005ad4b3adcbbe4b347857ced1232e79cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336412"
---
# <a name="ioreslist"></a>!ioreslist


**！ Ioreslist**扩展插件都会显示 IO\_资源\_要求\_列表结构。

```dbgcmd
!ioreslist Address 
```

## <a name="span-idddkioreslistdbgspanspan-idddkioreslistdbgspanparameters"></a><span id="ddk__ioreslist_dbg"></span><span id="DDK__IORESLIST_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的十六进制地址的 IO\_资源\_要求\_列表结构。

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

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关 IO\_资源\_要求\_列表结构中，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

下面是输出的来自此扩展插件示例：

```dbgcmd
kd> !ioreslist 0xe122b768

IoResList at 0xe122b768 : Interface 0x5  Bus 0  Slot 0xe
  Alternative 0 (Version 1.1)
    Preferred Descriptor 0 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_IO
      0x000100 byte range with alignment 0x000100
      1000 - 0x10ff
    Alternative Descriptor 1 - Port (0x1) Device Exclusive (0x1)
      Flags (0x01) - PORT_IO
      0x000100 byte range with alignment 0x000100
      0 - 0xffffffff
    Descriptor 2 - DevicePrivate (0x81) Device Exclusive (0x1)
      Flags (0000) -
      Data:              : 0x1 0x0 0x0
    Preferred Descriptor 3 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      0x001000 byte range with alignment 0x001000
      40080000 - 0x40080fff
    Alternative Descriptor 4 - Memory (0x3) Device Exclusive (0x1)
      Flags (0000) - READ_WRITE
      0x001000 byte range with alignment 0x001000
      0 - 0xffffffff
    Descriptor 5 - DevicePrivate (0x81) Device Exclusive (0x1)
      Flags (0000) -
      Data:              : 0x1 0x1 0x0
    Descriptor 6 - Interrupt (0x2) Shared (0x3)
      Flags (0000) - LEVEL_SENSITIVE
      0xb - 0xb
```

IO\_资源\_要求\_列表包含有关的信息：

-   资源类型

    有四种类型的资源：I/O, Memory, IRQ, DMA.

-   描述符

    每个首选的设置有"首选"描述符和"替代"说明符的数目。

此资源的列表包含以下请求：

-   I/O 范围

    倾向于一系列 0x1000 到 0x10FF 包含在内，但可以使用任何 0x100 介于 0 和 0xFFFFFFFF，前提是该 0x100 对齐。 （例如，0x1100 到 0x11FF 是可接受。）

-   内存

    倾向于一系列 0x40080000 到 0x40080FFF，但可以使用大小 0x1000 的是，是 0x1000 对齐，介于 0 和 0xFFFFFFFF 所在的任何范围。

-   IRQ

    必须使用 IRQ 0xB。

中断和 DMA 通道表示为具有相同的开始和结束范围。

 

 





