---
title: WDI_TLV_SAE_COMMIT_REQUEST
description: WDI_TLV_SAE_COMMIT_REQUEST 是一种 TLV，其中包含用于同时进行 Equals （SAE）提交请求的身份验证的参数。
ms.assetid: E339E58E-7929-416A-815D-C663EF1359D4
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_COMMIT_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7a4fd25037f7c315de65fe7ed4eb04df750f0b0c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918195"
---
# <a name="wdi_tlv_sae_commit_request"></a>WDI_TLV_SAE_COMMIT_REQUEST

**WDI_TLV_SAE_COMMIT_REQUEST**是一种 TLV，其中包含用于同时进行 EQUALS （SAE）提交请求的身份验证的参数。 

此 TLV 用于[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)的命令参数中。

## <a name="tlv-type"></a>TLV 类型

0x150

## <a name="length"></a>长度

所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值

| TLV | 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | UINT16 |   |   | 用于 SAE authentication 的有限循环组。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | TLV\<LIST\<UINT8>> |   |   | 有限字段元素（FFE）。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | TLV\<LIST\<UINT8>> |   |   | 已编码的字段元素（EFE）。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | TLV\<LIST\<UINT8>> |   |   | BSSID 请求的防堵塞令牌。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
