---
title: WDI_TLV_SAE_REQUEST_TYPE
description: WDI_TLV_SAE_REQUEST_TYPE 是一个 TLV，其中包含要发送到目标 BSSID 的 Equals （SAE）请求帧的同时身份验证类型。
ms.assetid: 90F0F7DA-DACA-49EF-86E8-CE4206D83882
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_REQUEST_TYPE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b7031c2121a376bb199fe94fdf2c1ef73f126b92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841741"
---
# <a name="wdi_tlv_sae_request_type"></a>WDI_TLV_SAE_REQUEST_TYPE

**WDI_TLV_SAE_REQUEST_TYPE**是一个 TLV，其中包含要发送到目标 BSSID 的 EQUALS （SAE）请求帧的同时身份验证类型。

此 TLV 用于[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)的命令参数。

## <a name="tlv-type"></a>TLV 类型

0x14F

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) | 要发送到 BSSID 的 SAE 请求帧的类型。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
