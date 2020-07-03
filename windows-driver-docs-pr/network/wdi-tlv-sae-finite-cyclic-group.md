---
title: WDI_TLV_SAE_FINITE_CYCLIC_GROUP
description: WDI_TLV_SAE_FINITE_CYCLIC_GROUP 是一个 TLV，其中包含提交请求中用于同时进行 Equals （SAE）身份验证的有限循环组。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_FINITE_CYCLIC_GROUP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cbeb5f051be1c84267f9036d984c908845630c81
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917131"
---
# <a name="wdi_tlv_sae_finite_cyclic_group"></a>WDI_TLV_SAE_FINITE_CYCLIC_GROUP

**WDI_TLV_SAE_FINITE_CYCLIC_GROUP**是一个 TLV，其中包含提交请求中用于同时进行 EQUALS （SAE）身份验证的有限循环组。

此 TLV 用于[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x152

## <a name="length"></a>长度

UINT16 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT16 | 用于 SAE authentication 的有限循环组。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
