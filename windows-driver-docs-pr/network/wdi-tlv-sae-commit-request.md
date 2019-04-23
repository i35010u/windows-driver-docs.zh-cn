---
title: WDI_TLV_SAE_COMMIT_REQUEST
description: WDI_TLV_SAE_COMMIT_REQUEST 是 TLV，其中包含同时进行身份验证的等于 (SAE) 提交请求的参数。
ms.assetid: E339E58E-7929-416A-815D-C663EF1359D4
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_COMMIT_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 45946a0051d2bfe0e26aeeaa5dbc3f025e457cdc
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905308"
---
# <a name="wditlvsaecommitrequest"></a>WDI_TLV_SAE_COMMIT_REQUEST

**WDI_TLV_SAE_COMMIT_REQUEST**是 TLV，其中包含同时进行身份验证的等于 (SAE) 提交请求的参数。 

中的命令参数使用此 TLV [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)。

## <a name="tlv-type"></a>TLV 类型

0x150

## <a name="length"></a>长度

所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | UINT16 |   |   | 用于 SAE 身份验证的有限循环组。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | TLV\<LIST\<UINT8>> |   |   | 有限的字段元素 (FFE) 中。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | TLV\<LIST\<UINT8>> |   |   | 编码的字段元素 (EFE) 中。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | TLV\<LIST\<UINT8>> |   |   | 作为请求的 BSSID 防 clogging 标记。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
