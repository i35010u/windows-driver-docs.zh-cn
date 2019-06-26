---
title: 查询端口状态
description: 查询端口状态
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- 端口状态 WDK NDIS
- 查询 NDIS 端口状态
- 端口 WDK NDIS OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6559d86cad14f7a569e96ae747dabd2ae9a12ccb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377026"
---
# <a name="querying-the-port-state"></a>查询端口状态





过量驱动程序可以发出[OID\_代\_端口\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)OID 查询请求以获取中指定的端口的当前状态**PortNumber**成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。 NDIS 接收端口的状态信息中[ **NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构。

OID\_GEN\_端口\_NDIS 6.0 和更高版本中支持状态 OID。

过量驱动程序应避免使用 OID\_GEN\_端口\_状态在可能的情况，应依赖于[ **NDIS\_状态\_端口\_状态** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状态指示。 有关端口相关的状态指示的详细信息，请参阅[处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)。

如果 OID\_GEN\_端口\_状态查询成功，则将 NDIS 返回中的端口状态信息[ **NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)结构。

 

 





