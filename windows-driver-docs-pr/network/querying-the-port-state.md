---
title: 查询端口状态
description: 查询端口状态
keywords:
- 端口状态 WDK NDIS
- 查询 NDIS 端口状态
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c591150ff26fb6127ede7fd65ab8fc2e18543916
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812839"
---
# <a name="querying-the-port-state"></a>查询端口状态





过量驱动程序可以发出 [oid \_ GEN \_ 端口 \_ 状态](./oid-gen-port-state.md)OID 查询请求，以获取在 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **PortNumber** 成员中指定的端口的当前状态。 NDIS 处理此 OID，微型端口驱动程序不会收到此 OID 查询。 NDIS 接收 [**ndis \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics) 结构中的端口状态信息。

\_ \_ \_ 在 NDIS 6.0 和更高版本中支持 oid GEN 端口状态 oid。

如果可能，过量驱动程序应避免使用 OID 生成 \_ \_ 端口 \_ 状态，并且应依赖 [**NDIS \_ 状态 \_ 端口 \_ 状态**](./ndis-status-port-state.md) 状态指示。 有关与端口相关的状态指示的详细信息，请参阅 [处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)。

如果 OID 生成 \_ \_ 端口 \_ 状态查询成功，Ndis 将返回 [**ndis \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state) 结构中的端口状态信息。

 

