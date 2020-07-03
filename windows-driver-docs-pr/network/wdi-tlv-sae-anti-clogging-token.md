---
title: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
description: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 是一种 TLV，其中包含用于同时身份验证 Equals （SAE）提交请求的防堵塞令牌。
ms.assetid: 9A1046AE-029F-4B37-9523-655425BC93F1
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bf97fbce6360f1f7c2f4839b921cec220f0cb03d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916891"
---
# <a name="wdi_tlv_sae_anti_clogging_token"></a>WDI_TLV_SAE_ANTI_CLOGGING_TOKEN

**WDI_TLV_SAE_ANTI_CLOGGING_TOKEN**是一种 TLV，其中包含用于同时身份验证 EQUALS （SAE）提交请求的防堵塞令牌。

此 TLV 用于[WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x155

## <a name="length"></a>长度

UINT8 元素数组的大小（以字节为单位）。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 [] | 防堵塞标记。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
