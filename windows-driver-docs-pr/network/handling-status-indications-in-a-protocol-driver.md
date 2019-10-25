---
title: 处理协议驱动程序中的状态指示
description: 处理协议驱动程序中的状态指示
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a07d7ac61015f5bfcb6d10f0169be859a7ef1a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842556"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>处理协议驱动程序中的状态指示





协议驱动程序必须提供一个[**ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)函数，NDIS 在基础驱动程序报告状态时调用该函数。

在基础驱动程序调用状态指示函数（[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))或[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)）之后，NDIS 调用协议驱动程序的*ProtocolStatusEx*函数。 有关从微型端口驱动程序指示状态的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

有关从筛选器驱动程序指示状态的详细信息，请参阅[筛选模块状态指示](filter-module-status-indications.md)。

如果状态指示与 OID 请求关联，则基础驱动程序可以设置**DestinationHandle**和**RequestId**成员，使 NDIS 能够向特定协议绑定提供状态指示。 有关 OID 请求的详细信息，请参阅[协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

 

 





