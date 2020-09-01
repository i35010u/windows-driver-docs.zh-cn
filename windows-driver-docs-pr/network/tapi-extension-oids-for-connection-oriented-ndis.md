---
title: 面向连接的 NDIS 的 TAPI 扩展 OID
description: 本主题介绍面向连接的 NDIS 的 TAPI 扩展 Oid。
ms.assetid: 06f7e2d0-b890-468e-8177-d3c28d0e9cd0
keywords:
- TAPI 扩展 Oid 面向连接的 NDIS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9fe3c95edfde862bb5029991880b15d4ff473e1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212727"
---
# <a name="tapi-extension-oids-for-connection-oriented-ndis"></a>面向连接的 NDIS 的 TAPI 扩展 OID

下表汇总了允许通过面向连接的媒体进行 TAPI 调用的 Oid。 面向连接的客户端将这些 Oid 发送给调用管理器 (MCM) 驱动程序的集成微型端口调用管理器。

在此表中，M 指示 OID 是必需的，而 O 指示它是可选的。

| Length | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 多种多样 | O |   | [OID_CO_TAPI_ADDRESS_CAPS](oid-co-tapi-address-caps.md) |
| Sizeof (CO_TAPI_CM_CAPS)  | O |   | [OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md) |
| 多种多样 | O |   | [OID_CO_TAPI_GET_CALL_DIAGNOSTICS](oid-co-tapi-get-call-diagnostics.md) |
| 多种多样 | O |   | [OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md) |
| 多种多样 | O |   | [OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS](oid-co-tapi-translate-ndis-callparams.md) |
| 多种多样 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS](oid-co-tapi-translate-tapi-callparams.md) |
| 多种多样 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_SAP](oid-co-tapi-translate-tapi-sap.md) |

在调用 [NdisCoRequest](/previous-versions/windows/hardware/network/ff551877(v=vs.85))时，查询任何 TAPI 扩展 oid 的客户端必须指定一个 *NdisAfHandle* ，用于标识请求应用到的地址族。 客户端可以指定 *NdisVcHandle* ，用于标识请求应用到的虚拟连接 (VC) 。 通过此 VC 句柄，调用管理器或 MCM 驱动程序可以派生特定的行，可能还可以派生请求应用到的地址。