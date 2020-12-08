---
title: OID_GEN_CO_MEDIA_IN_USE
description: 本主题介绍) OID_GEN_CO_MEDIA_IN_USE 对象标识符 (OID。
keywords:
- OID_GEN_CO_MEDIA_IN_USE
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94f7f9562954ae13a14debf642a6f0a8d64a9498
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806163"
---
# <a name="oid_gen_co_media_in_use"></a>OID_GEN_CO_MEDIA_IN_USE

NIC 当前支持的介质类型的完整列表，定义为 "某些"、"无" (也称为 "NULL 筛选器) " 或以下所有内容：

**NdisMedium802_3**  
以太网 (802.3) 。

**NdisMedium802_5**  
 (802.5) 的令牌环。

**NdisMediumFddi**  
FDDI.

**NdisMediumWan**  
WAN.

**NdisMediumLocalTalk**  
LocalTalk.

**NdisMediumDix**  
DIX.

**NdisMediumArcnetRaw**  
ARCNET (原始) 。

**NdisMediumArcnet878_2**  
ARCNET (878.2) 。

**NdisMediumWirelessWan**  
各种类型的 NdisWirelessXxx 媒体。

**NdisMediumAtm**  
ATM.

如果基础微型端口驱动程序为此查询返回 **NULL** ，或者如果使用的是实验媒体类型，则驱动程序必须使用 [NdisMCoIndicateReceivePacket](/previous-versions/windows/hardware/network/ff553455(v=vs.85))指示接收。


## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
