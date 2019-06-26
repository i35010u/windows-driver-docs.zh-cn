---
title: OID_GEN_CO_MEDIA_IN_USE
description: 本主题介绍 OID_GEN_CO_MEDIA_IN_USE 对象标识符 (OID)。
ms.assetid: 59a2c981-87a5-4df9-af26-3c5a5eadc17a
keywords:
- OID_GEN_CO_MEDIA_IN_USE
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eb974aeb0ff8cb421077c3122d60069e5f19509
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361182"
---
# <a name="oidgencomediainuse"></a>OID_GEN_CO_MEDIA_IN_USE

当前支持的 NIC 的媒体类型的完整列表定义为一些、 none （也称为 NULL 筛选器），或所有以下：

**NdisMedium802_3**  
以太网 (802.3)。

**NdisMedium802_5**  
令牌环 (802.5)。

**NdisMediumFddi**  
FDDI。

**NdisMediumWan**  
WAN。

**NdisMediumLocalTalk**  
LocalTalk。

**NdisMediumDix**  
DIX。

**NdisMediumArcnetRaw**  
ARCNET （原始）。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
各种类型的 NdisWirelessXxx 媒体。

**NdisMediumAtm**  
ATM。

如果基础微型端口驱动程序将返回**NULL**此查询或如果使用实验性的媒体类型，必须指示驱动程序将会收到包含[NdisMCoIndicateReceivePacket](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553455(v=vs.85))。


## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

