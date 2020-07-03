---
title: WDI_TLV_SAE_SEND_CONFIRM
description: WDI_TLV_SAE_SEND_CONFIRM 是一种 TLV，其中包含对 Equals （SAE）确认请求同时进行的身份验证的发送确认字段。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_SEND_CONFIRM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 901946f9867bca33af52a4358ec041429c2c77d0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918287"
---
# <a name="wdi_tlv_sae_send_confirm"></a>WDI_TLV_SAE_SEND_CONFIRM

**WDI_TLV_SAE_SEND_CONFIRM**是一种 TLV，其中包含对 EQUALS （SAE）确认请求同时进行的身份验证的发送确认字段。 "发送确认" 字段用作反重播计数器。

此 TLV 用于[WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x156

## <a name="length"></a>长度

UINT16 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT16 | 发送确认字段。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
