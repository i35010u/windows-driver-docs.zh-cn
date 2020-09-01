---
title: 处理协议驱动程序中的状态指示
description: 处理协议驱动程序中的状态指示
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f13e026ef43a5e06e578e3eb29942e3899c00ae
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211067"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>处理协议驱动程序中的状态指示





协议驱动程序必须提供一个 [**ProtocolStatusEx**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex) 函数，NDIS 在基础驱动程序报告状态时调用该函数。

在基础驱动程序 ([**NdisMIndicateStatus**](/previous-versions/windows/hardware/network/ff553538(v=vs.85))或[**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)) 调用状态指示函数后，NDIS 将调用一个协议驱动程序的*ProtocolStatusEx*函数。 有关从微型端口驱动程序指示状态的详细信息，请参阅 [适配器状态指示](miniport-adapter-status-indications.md)。

有关从筛选器驱动程序指示状态的详细信息，请参阅 [筛选模块状态指示](filter-module-status-indications.md)。

如果状态指示与 OID 请求关联，则基础驱动程序可以设置 **DestinationHandle** 和 **RequestId** 成员，使 NDIS 能够向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅 [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

 

