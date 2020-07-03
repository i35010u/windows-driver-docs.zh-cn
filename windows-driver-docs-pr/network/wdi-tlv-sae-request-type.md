---
title: WDI_TLV_SAE_REQUEST_TYPE
description: WDI_TLV_SAE_REQUEST_TYPE 是一种 TLV，其中包含要发送到目标 BSSID 的 Equals （SAE）请求帧的同时身份验证类型。
ms.assetid: 90F0F7DA-DACA-49EF-86E8-CE4206D83882
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_REQUEST_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5212ff147a514237108f06389dcb8b7bdedf8de6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918105"
---
# <a name="wdi_tlv_sae_request_type"></a>WDI_TLV_SAE_REQUEST_TYPE

**WDI_TLV_SAE_REQUEST_TYPE**是一种 TLV，其中包含要发送到目标 BSSID 的 EQUALS （SAE）请求帧的同时身份验证类型。

此 TLV 用于[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)的命令参数中。

## <a name="tlv-type"></a>TLV 类型

0x14F

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) | 要发送到 BSSID 的 SAE 请求帧的类型。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
