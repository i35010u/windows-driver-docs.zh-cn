---
title: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
description: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 是一种 TLV，其中包含用于同时进行的身份验证（等于 (SAE) 提交请求）的防堵塞令牌。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 349ebee96d3dd2699fe2979eaf64344a77bd5692
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834237"
---
# <a name="wdi_tlv_sae_anti_clogging_token"></a>WDI_TLV_SAE_ANTI_CLOGGING_TOKEN

**WDI_TLV_SAE_ANTI_CLOGGING_TOKEN** 是一种 TLV，其中包含用于同时进行的身份验证（等于 (SAE) 提交请求）的防堵塞令牌。

此 TLV 用于 [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x155

## <a name="length"></a>长度

UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 [] | 防堵塞标记。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
