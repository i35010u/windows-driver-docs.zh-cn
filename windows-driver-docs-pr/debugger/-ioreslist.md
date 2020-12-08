---
title: ioreslist
description: Ioreslist 扩展显示 IO_RESOURCE_REQUIREMENTS_LIST 结构。
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
ms.openlocfilehash: e8202145b2485a1b9e10b96dce438914b912f71e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788943"
---
# <a name="ioreslist"></a>!ioreslist


**！ Ioreslist** 扩展显示 IO \_ 资源 \_ 需求 \_ 列表结构。

```dbgcmd
!ioreslist Address 
```

## <a name="span-idddk__ioreslist_dbgspanspan-idddk__ioreslist_dbgspanparameters"></a><span id="ddk__ioreslist_dbg"></span><span id="DDK__IORESLIST_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 IO \_ 资源 \_ 需求列表结构的十六进制地址 \_ 。

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

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关 IO \_ 资源 \_ 需求 \_ 列表结构的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

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

IO \_ 资源 \_ 需求 \_ 列表包含以下信息：

-   资源类型

    有四种类型的资源： i/o、内存、IRQ、DMA。

-   描述符

    每个首选设置都有 "首选" 描述符和多个 "备用" 描述符。

此资源列表包含以下请求：

-   I/o 范围

    首选范围为0x10FF，但可以使用0到0xFFFFFFFF 之间的任何0x100 范围，前提是它是0x100 对齐的。  (例如，可接受0x1100 到0x11FF。 ) 

-   内存

    首选0x40080000 到0x40080FFF 的范围，但可以使用大小为0x1000 的任何范围，大小为0x1000，并位于0到0xFFFFFFFF 之间。

-   IRQ

    必须使用 IRQ 0xB。

中断和 DMA 通道表示为具有相同开始和结束的范围。

 

 





