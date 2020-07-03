---
title: OID_GEN_CO_SUPPORTED_LIST
description: 本主题介绍 OID_GEN_CO_SUPPORTED_LIST 对象标识符（OID）。
ms.assetid: 51c2b7f5-8429-4609-b048-542a3509f645
keywords:
- OID_GEN_CO_SUPPORTED_LIST
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c711692d10de29fe375c1769b6034ec1bd45f615
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917027"
---
# <a name="oid_gen_co_supported_list"></a>OID_GEN_CO_SUPPORTED_LIST

OID_GEN_CO_SUPPORTED_LIST OID 为基础驱动程序或其 NIC 支持的对象指定 Oid 数组。 对象包括常规、特定于媒体和特定于实现的对象。

底层驱动程序应按照递增的数值顺序对 OID 列表进行排序。 NDIS 将返回列表的一个子集转发到执行此查询的协议。 也就是说，NDIS 筛选出列表中任何受支持的统计信息

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

