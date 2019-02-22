---
title: ndiskd.findpacket
description: 警告此扩展适用于旧 NDIS 5.x 驱动程序。 已弃用 NDIS_PACKET 结构和其关联的体系结构。 Ndiskd.findpacket 扩展查找指定的数据包。
ms.assetid: fc07b2d8-85ca-4be1-ae9d-40b7c7f81b08
keywords:
- ndiskd.findpacket Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.findpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9debfc45c946987dc72a585edaae2f7e445e217b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541379"
---
# <a name="ndiskdfindpacket"></a>!ndiskd.findpacket


**警告**  此扩展是旧的 NDIS 5.x 驱动程序。 [NDIS\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff557086)结构和其关联的体系结构已被弃用。

 

**！ Ndiskd.findpacket**扩展查找指定的数据包。

```console
!ndiskd.findpacket [-VirtualAddress] [-PoolAddress]  
```

## <a name="span-idddkndiskdfindpacketdbgspanspan-idddkndiskdfindpacketdbgspanparameters"></a><span id="ddk__ndiskd_findpacket_dbg"></span><span id="DDK__NDISKD_FINDPACKET_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *VirtualAddress*   
指定在所需的包中包含的虚拟地址。

<span id="_______PoolAddress______"></span><span id="_______pooladdress______"></span><span id="_______POOLADDRESS______"></span> *PoolAddress*   
指定池的地址。 将显示此池中的所有 unreturned 的数据包。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅

[NDIS\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff557086)

 

 






