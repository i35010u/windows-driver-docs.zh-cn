---
title: ndiskd
description: 警告此扩展适用于旧的 NDIS 1.x 驱动程序。Ndiskd 扩展显示 NDIS_PACKET 结构的相关信息。
ms.assetid: 8e704173-3b09-4377-b73a-ba67a3c3c930
keywords:
- ndiskd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pkt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7ebd9577322e55337316d8c52e66ad165732dfd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209887"
---
# <a name="ndiskdpkt"></a>!ndiskd.pkt

**警告**   此扩展适用于旧的 NDIS 1.x 驱动程序。 [NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构及其关联的体系结构已弃用。

**！ Ndiskd** extension 显示有关[NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))结构的信息。

```console
!ndiskd.pkt [-packet] [-verbosity] 
```

## <a name="parameters"></a>参数

<span id="_______Packet______"></span><span id="_______packet______"></span><span id="_______PACKET______"></span>*数据包*   
指定数据包的地址。

<span id="_______Verbosity______"></span><span id="_______verbosity______"></span><span id="_______VERBOSITY______"></span>*详细级别*   
指定要显示的详细信息的数量。

### <a name="dll"></a>DLL

Ndiskd.dll

## <a name="see-also"></a>另请参阅

[NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85))