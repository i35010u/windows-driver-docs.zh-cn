---
title: OID_GEN_CO_MEDIA_SUPPORTED
description: 本主题介绍 OID_GEN_CO_MEDIA_SUPPORTED 对象标识符 (OID)。
ms.assetid: 688d5054-f92d-4054-bf6e-dcf43fcfeb06
keywords:
- OID_GEN_CO_MEDIA_SUPPORTED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b473639e3788c38c876d7d116da1db5f29b6a97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542073"
---
# <a name="oidgencomediasupported"></a>OID_GEN_CO_MEDIA_SUPPORTED

媒体的完整列表类型 NIC 支持中，定义为以下系统定义的值的真子集：

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
DEC/Intel Xerox (DIX) 以太网。

**NdisMediumArcnetRaw**  
ARCNET （原始）。

**NdisMediumArcnet878_2**  
ARCNET (878.2)。

**NdisMediumWirelessWan**  
各种类型的 NdisWirelessXxx 媒体。

**NdisMediumAtm**  
ATM。

**NdisMediumIrda**  
保留供将来使用在 Windows 2000 和更高版本的平台上。

## <a name="remarks"></a>备注

ATM 网络 LAN 仿真驱动程序声明为其中等**NdisMedium802_3** ，而非**NdisMediumAtm**。 这样的驱动程序模拟以太网更高级别的的 NDIS 驱动程序，符合 ATM 论坛通道，并提供单元信号的支持。

WAN 无线 NIC 驱动程序必须报告为其介质类型**NdisMediumWirelessWan**。 但是，这样的微型端口驱动程序还必须提供**NdisWWDIXEthernetFrames**标头格式到任何绑定选择此格式的协议和微型端口驱动程序可以提供其 NIC 的纯标头格式以及。 若要支持现有基于 LAN 的协议，驱动程序编写器可以提供 NDIS 中间驱动程序"翻译"无线 NIC 的纯标头格式和到理解现有协议的一个窗体的特定于中的信息。

如果基础微型端口驱动程序将返回**NULL**此查询或如果使用实验性的媒体类型，必须指示驱动程序将会收到包含[NdisMCoIndicateReceivePacket](https://msdn.microsoft.com/library/windows/hardware/ff553455)。


## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

