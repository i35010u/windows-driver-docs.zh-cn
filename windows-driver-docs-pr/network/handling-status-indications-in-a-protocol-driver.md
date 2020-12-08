---
title: 处理协议驱动程序中的状态指示
description: 处理协议驱动程序中的状态指示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e89da2dec942e9d14a34d175d03297625fe4dfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794544"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>处理协议驱动程序中的状态指示





协议驱动程序必须提供一个 [**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) 函数，NDIS 在基础驱动程序报告状态时调用该函数。

在基础驱动程序 ([**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))或 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)) 调用状态指示函数后，NDIS 将调用一个协议驱动程序的 *ProtocolStatusEx* 函数。 有关从微型端口驱动程序指示状态的详细信息，请参阅 [适配器状态指示](miniport-adapter-status-indications.md)。

有关从筛选器驱动程序指示状态的详细信息，请参阅 [筛选模块状态指示](filter-module-status-indications.md)。

如果状态指示与 OID 请求关联，则基础驱动程序可以设置 **DestinationHandle** 和 **RequestId** 成员，使 NDIS 能够向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅 [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

 

