---
title: ndiskd.pktpools
description: 警告此扩展适用于旧 NDIS 5.x 驱动程序。 Ndiskd.pktpools 扩展显示所有已分配的数据包池的列表。
ms.assetid: 0aceb22c-17ab-4199-a313-ecbc4c8f0b6e
keywords:
- ndiskd.pktpools Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pktpools
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3953c94e9d9c586c723f50eae444a803c5c8dbb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362457"
---
# <a name="ndiskdpktpools"></a>!ndiskd.pktpools


**警告**  此扩展是旧的 NDIS 5.x 驱动程序。 [NDIS\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构和其关联的体系结构已被弃用。

 

**！ Ndiskd.pktpools**扩展插件都会显示所有已分配的数据包池的列表。

```console
!ndiskd.pktpools 
```

## <span id="ddk__ndiskd_pktpools_dbg"></span><span id="DDK__NDISKD_PKTPOOLS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.pktpools**扩展以在系统上查看所有已分配的数据包池的列表。 请注意，数据包池的句柄不是可单击，这意味着你不能浏览数据包池的详细信息。 这是因为 NDIS 不使用从 NDIS 6.0 开始，因此这些池分配仅对旧驱动程序可能仍是较旧的系统上的数据包池。 在此示例中的调试对象计算机不具有任何旧的 NDIS 5.x 驱动程序安装，以便不使用数据包池。 此示例是仅供说明用途。

```console
3: kd> !ndiskd.pktpools
Pool      Allocator  BlocksAllocated  BlockSize  PktsPerBlock  PacketLength
ffffdf80131d58c0  fffff80f1fbe3e8f   0x1          0x1000     0xa           0x190   ndis!DriverEntry+6af
ffffdf80131d5940  fffff80f1fbe3e71   0x1          0x1000     0xa           0x180   ndis!DriverEntry+691
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[Windows 2000 和 Windows XP 网络设计指南](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))

[Windows 2000 和 Windows XP 网络参考](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565850(v=vs.85))

[NDIS\_数据包](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))

 

 






