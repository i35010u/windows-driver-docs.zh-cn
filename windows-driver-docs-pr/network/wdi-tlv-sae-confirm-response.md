---
title: WDI_TLV_SAE_COMMIT_RESPONSE
description: WDI_TLV_SAE_CONFIRM_RESPONSE 是一种 TLV，其中包含等于 (SAE) 确认响应帧的同时身份验证。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5d6ddcfc4545689b53123bdaf670c250bfcf836c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834225"
---
# <a name="wdi_tlv_sae_confirm_response"></a>WDI_TLV_SAE_COMMIT_RESPONSE

**WDI_TLV_SAE_CONFIRM_RESPONSE** 是一种 TLV，其中包含等于 (SAE) 确认响应帧的同时身份验证。

此 TLV 在 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中使用。

## <a name="tlv-type"></a>TLV 类型

0x14E

## <a name="length"></a>长度

UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 [] | SAE 确认响应帧。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
