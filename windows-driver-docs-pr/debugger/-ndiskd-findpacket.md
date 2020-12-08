---
title: ndiskd.findpacket
description: 警告此扩展适用于旧的 NDIS 1.x 驱动程序。 NDIS_PACKET 结构及其关联的体系结构已弃用。 Ndiskd. findpacket 扩展查找指定的数据包。
keywords:
- ndiskd findpacket Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.findpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29225b94c838c6c54993b4c8008cf36c15d14a69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796323"
---
# <a name="ndiskdfindpacket"></a>!ndiskd.findpacket

**警告**  此扩展适用于旧的 NDIS 1.x 驱动程序。 [NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构及其关联的体系结构已弃用。

**！ Ndiskd findpacket** 扩展查找指定的数据包。

```console
!ndiskd.findpacket [-VirtualAddress] [-PoolAddress]  
```

## <a name="parameters"></a>参数

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*VirtualAddress*   
指定所需数据包中包含的虚拟地址。

<span id="_______PoolAddress______"></span><span id="_______pooladdress______"></span><span id="_______POOLADDRESS______"></span>*PoolAddress*   
指定池地址。 将显示此池中的所有 unreturned 数据包。

### <a name="dll"></a>DLL

Ndiskd.dll

## <a name="see-also"></a>请参阅

[NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))
