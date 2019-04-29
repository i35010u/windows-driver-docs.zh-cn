---
title: 面向连接的 NDIS 的 TAPI 扩展 OID
description: 本主题介绍面向连接的 NDIS TAPI 扩展 Oid。
ms.assetid: 06f7e2d0-b890-468e-8177-d3c28d0e9cd0
keywords:
- TAPI 扩展 Oid 面向连接的 NDIS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c5a2735e5ec011bdbbe16e442a04979ecf671cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378724"
---
# <a name="tapi-extension-oids-for-connection-oriented-ndis"></a>面向连接的 NDIS 的 TAPI 扩展 OID

下表总结了允许 TAPI 调用通过面向连接的媒体进行的 Oid。 面向连接的客户端发送这些 Oid 来调用管理器或集成的微型端口呼叫管理器 (MCM) 驱动程序。

在此表中，M 指示 OID 是必需的而 O 则指示它是可选的。

| 长度 | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 变化不定 | O |   | [OID_CO_TAPI_ADDRESS_CAPS](oid-co-tapi-address-caps.md) |
| Sizeof(CO_TAPI_CM_CAPS) | O |   | [OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md) |
| 变化不定 | O |   | [OID_CO_TAPI_GET_CALL_DIAGNOSTICS](oid-co-tapi-get-call-diagnostics.md) |
| 变化不定 | O |   | [OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md) |
| 变化不定 | O |   | [OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS](oid-co-tapi-translate-ndis-callparams.md) |
| 变化不定 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS](oid-co-tapi-translate-tapi-callparams.md) |
| 变化不定 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_SAP](oid-co-tapi-translate-tapi-sap.md) |

对其调用中[NdisCoRequest](https://msdn.microsoft.com/library/windows/hardware/ff551877)，查询任何 TAPI 扩展 Oid 的客户端必须指定*NdisAfHandle* ，用于标识请求应用到的地址族。 客户端可以指定*NdisVcHandle*用于标识虚拟连接 (VC) 向其请求的应用。 VC 此句柄，从呼叫管理器或 MCM 驱动程序可能能够派生特定行和可能是请求应用到的地址。

