---
title: OID_GEN_CO_MEDIA_SUPPORTED
description: 本主题介绍) OID_GEN_CO_MEDIA_SUPPORTED 对象标识符 (OID。
ms.assetid: 688d5054-f92d-4054-bf6e-dcf43fcfeb06
keywords:
- OID_GEN_CO_MEDIA_SUPPORTED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76afbb04a68b5306edf690de8fe464b4b0e988e6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215486"
---
# <a name="oid_gen_co_media_supported"></a>OID_GEN_CO_MEDIA_SUPPORTED

NIC 支持的介质类型的完整列表，作为以下系统定义的值的正确子集：

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
DEC/Intel/Xerox (DIX) 以太网。

**NdisMediumArcnetRaw**  
ARCNET (原始) 。

**NdisMediumArcnet878_2**  
ARCNET (878.2) 。

**NdisMediumWirelessWan**  
各种类型的 NdisWirelessXxx 媒体。

**NdisMediumAtm**  
ATM.

**NdisMediumIrda**  
保留以供将来用于 Windows 2000 和更高版本的平台。

## <a name="remarks"></a>备注

ATM 网络的 LAN 仿真驱动程序将其媒体声明为 **NdisMedium802_3** ，而不是 **NdisMediumAtm**。 此类驱动程序将以太网模拟到更高级别的 NDIS 驱动程序，符合 ATM 论坛的 LANE，并提供单信号支持。

无线 WAN NIC 驱动程序必须将其中型类型报告为 **NdisMediumWirelessWan**。 但是，这种微型端口驱动程序还必须为选择此格式的任何绑定协议提供 **NdisWWDIXEthernetFrames** 标头格式，而微型端口驱动程序也可以提供其 NIC 的本机标头格式。 为了支持现有的基于 LAN 的协议，驱动程序编写器可以提供一个 NDIS 中间驱动程序，以将无线 NIC 的本机标头格式和特定于中型的信息转换为现有协议理解的形式。

如果基础微型端口驱动程序为此查询返回 **NULL** ，或者如果使用的是实验媒体类型，则驱动程序必须使用 [NdisMCoIndicateReceivePacket](/previous-versions/windows/hardware/network/ff553455(v=vs.85))指示接收。


## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 