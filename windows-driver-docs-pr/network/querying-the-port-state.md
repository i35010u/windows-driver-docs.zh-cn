---
title: 查询端口状态
description: 查询端口状态
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- 端口状态 WDK NDIS
- 查询 NDIS 端口状态
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccb894eda118b71b33ca678bfadafe555e2df4e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844866"
---
# <a name="querying-the-port-state"></a>查询端口状态





过量驱动程序可以[\_GEN\_\_端口发出 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state) ，以获取在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**PortNumber**成员中指定的端口的当前状态。 NDIS 处理此 OID，微型端口驱动程序不会收到此 OID 查询。 NDIS [ **\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构中接收端口状态信息。

在 NDIS 6.0 和更高版本中支持 OID\_GEN\_端口\_状态 OID。

如果可能，过量驱动程序应避免使用 OID\_代\_端口\_状态，应改为依赖[**NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状态指示。 有关与端口相关的状态指示的详细信息，请参阅[处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)。

如果 OID\_GEN\_端口\_状态查询成功，NDIS 将返回[**ndis\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)结构中的端口状态信息。

 

 





