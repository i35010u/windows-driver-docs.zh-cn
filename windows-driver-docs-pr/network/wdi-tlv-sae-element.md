---
title: WDI_TLV_SAE_ELEMENT
description: WDI_TLV_SAE_ELEMENT 是一个 TLV，其中包含已编码的字段元素（EFE），用于对 Equals （SAE）提交请求同时进行身份验证。
ms.assetid: B5E4DC7A-40B5-4F1D-A1C5-D2526FA0DF4D
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_ELEMENT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1244433d21a586bb425964f9adfee38e95899272
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916385"
---
# <a name="wdi_tlv_sae_element"></a>WDI_TLV_SAE_ELEMENT

**WDI_TLV_SAE_ELEMENT**是一个 TLV，其中包含已编码的字段元素（EFE），用于对 EQUALS （SAE）提交请求同时进行身份验证。

此 TLV 用于[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x154

## <a name="length"></a>长度

UINT8 元素数组的大小（以字节为单位）。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 [] | EFE 的一部分。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
