---
title: ndiskd.pktpools
description: 警告此扩展适用于旧的 NDIS 1.x 驱动程序。 Ndiskd. pktpools 扩展显示所有已分配的数据包池的列表。
keywords:
- ndiskd pktpools Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pktpools
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50e516ff15034c44243f143dadcd3112578ceab1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813335"
---
# <a name="ndiskdpktpools"></a>!ndiskd.pktpools

**警告**  此扩展适用于旧的 NDIS 1.x 驱动程序。 [NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构及其关联的体系结构已弃用。

**！ Ndiskd pktpools** 扩展显示所有已分配的数据包池的列表。

```console
!ndiskd.pktpools
```

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

运行 **！ ndiskd. pktpools** 扩展，以查看系统上所有已分配的数据包池的列表。 请注意，数据包池的句柄不可单击，这意味着你无法浏览有关数据包池的进一步信息。 这是因为，NDIS 不使用从 NDIS 6.0 开始的数据包池，因此这些池仅分配给可能仍在较早的系统上的旧驱动程序。 本示例中的调试对象计算机未安装任何旧版 NDIS 1.x 驱动程序，因此不使用数据包池。 此示例仅用于说明目的。

```console
3: kd> !ndiskd.pktpools
Pool      Allocator  BlocksAllocated  BlockSize  PktsPerBlock  PacketLength
ffffdf80131d58c0  fffff80f1fbe3e8f   0x1          0x1000     0xa           0x190   ndis!DriverEntry+6af
ffffdf80131d5940  fffff80f1fbe3e71   0x1          0x1000     0xa           0x180   ndis!DriverEntry+691
```

## <a name="see-also"></a>请参阅

[Windows 2000 和 Windows XP 网络设计指南](/previous-versions/windows/hardware/network/ff565849(v=vs.85))

[Windows 2000 和 Windows XP 网络参考](/previous-versions/windows/hardware/network/ff565850(v=vs.85))

[NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))
