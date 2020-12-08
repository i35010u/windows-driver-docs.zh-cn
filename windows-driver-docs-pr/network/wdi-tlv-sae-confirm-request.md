---
title: WDI_TLV_SAE_COMMIT_REQUEST
description: WDI_TLV_SAE_CONFIRM_REQUEST 是一种 TLV，其中包含对等 (SAE) 确认请求的同时身份验证的参数。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ccedc54537afe5a8e15a839a841cadbe21fa140e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817995"
---
# <a name="wdi_tlv_sae_confirm_request"></a>WDI_TLV_SAE_COMMIT_REQUEST

**WDI_TLV_SAE_CONFIRM_REQUEST** 是一种 TLV，其中包含对等 (SAE) 确认请求的同时身份验证的参数。 

此 TLV 用于 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)的命令参数中。

## <a name="tlv-type"></a>TLV 类型

0x151

## <a name="length"></a>长度

Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值

| TLV | 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | UINT16 |   |   | 发送确认字段，用作反重播计数器。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | TLV\<LIST\<UINT8>> |  |   | 确认字段。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
