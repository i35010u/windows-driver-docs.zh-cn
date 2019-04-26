---
title: 处理协议驱动程序中的状态指示
description: 处理协议驱动程序中的状态指示
ms.assetid: 1a021919-fd27-49b2-95a0-5ccb9029abd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eba1b6cc8279c844ed15e36f14c43879cab2679
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325719"
---
# <a name="handling-status-indications-in-a-protocol-driver"></a>处理协议驱动程序中的状态指示





协议驱动程序必须提供[ **ProtocolStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570270) NDIS 调用时基础驱动程序将状态报告函数。

NDIS 调用协议驱动程序*ProtocolStatusEx*基础驱动程序调用的状态指示函数后正常 ([**NdisMIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff553538)或[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824))。 指示从微型端口驱动程序状态的详细信息，请参阅[适配器状态指示](miniport-adapter-status-indications.md)。

指示从筛选器驱动程序状态的详细信息，请参阅[筛选器模块状态指示](filter-module-status-indications.md)。

如果状态指示是使用 OID 请求相关联，可以设置基础驱动程序**DestinationHandle**并**RequestId**成员，因此该 NDIS 可以提供与特定的状态指示协议绑定。 有关 OID 的请求的详细信息，请参阅[协议驱动程序 OID 请求](protocol-driver-oid-requests.md)。

 

 





