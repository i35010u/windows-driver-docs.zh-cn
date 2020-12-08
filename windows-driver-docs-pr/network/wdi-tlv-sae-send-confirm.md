---
title: WDI_TLV_SAE_SEND_CONFIRM
description: WDI_TLV_SAE_SEND_CONFIRM 是一种 TLV，其中包含等于 (SAE) 确认请求的同时身份验证的发送确认字段。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_SEND_CONFIRM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 448cc9e5eef9670d0276415e75e9ce32bcfbddaf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834197"
---
# <a name="wdi_tlv_sae_send_confirm"></a>WDI_TLV_SAE_SEND_CONFIRM

**WDI_TLV_SAE_SEND_CONFIRM** 是一种 TLV，其中包含等于 (SAE) 确认请求的同时身份验证的发送确认字段。 "发送确认" 字段用作反重播计数器。

此 TLV 用于 [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x156

## <a name="length"></a>长度

UINT16) 大小 (（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT16 | 发送确认字段。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
