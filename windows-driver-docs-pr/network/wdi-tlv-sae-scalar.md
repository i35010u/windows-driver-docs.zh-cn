---
title: WDI_TLV_SAE_SCALAR
description: WDI_TLV_SAE_SCALAR 是一种 TLV，其中包含对 Equals （SAE）提交请求同时进行的身份验证的有限字段元素（FFE）。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_SCALAR 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a5823b4f11a4b5d3bae1cba9afe173ed8572fca2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918101"
---
# <a name="wdi_tlv_sae_scalar"></a>WDI_TLV_SAE_SCALAR

**WDI_TLV_SAE_SCALAR**是一种 TLV，其中包含对 EQUALS （SAE）提交请求同时进行的身份验证的有限字段元素（FFE）。

此 TLV 用于[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x153

## <a name="length"></a>长度

UINT8 元素数组的大小（以字节为单位）。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 [] | FFE。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
