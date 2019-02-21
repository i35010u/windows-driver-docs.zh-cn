---
title: OID_GEN_CO_SUPPORTED_LIST
description: 本主题介绍 OID_GEN_CO_SUPPORTED_LIST 对象标识符 (OID)。
ms.assetid: 51c2b7f5-8429-4609-b048-542a3509f645
keywords:
- OID_GEN_CO_SUPPORTED_LIST
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: f053e840ecc7994dbe7c8a0e94c9b04213bbacea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548281"
---
# <a name="oidgencosupportedlist"></a>OID_GEN_CO_SUPPORTED_LIST

OID_GEN_CO_SUPPORTED_LIST OID 指定基础驱动程序或其 NIC 支持的对象的 Oid 的数组。 对象包括常规、 媒体特定和特定于实现的对象。

基础驱动程序应返回中递增的数字顺序对 OID 列表排序。 NDIS 将转发到协议，使此查询返回的列表的子集。 即 NDIS 筛选任何受支持的统计信息 Oid 的列表，因为协议永远不会随后进行统计信息的查询。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

