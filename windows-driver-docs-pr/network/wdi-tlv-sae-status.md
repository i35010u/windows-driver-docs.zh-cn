---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS 是一个 TLV，其中包含 Equals （SAE）身份验证失败错误状态的同时身份验证。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_STATUS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f3f48f0a490a06908a85320c004a04783641758a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841737"
---
# <a name="wdi_tlv_sae_status"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**是一个 TLV，其中包含 EQUALS （SAE）身份验证失败错误状态的同时身份验证。

此 TLV 用于[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)的命令参数和[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中。

## <a name="tlv-type"></a>TLV 类型

0x14C

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) | SAE authentication 失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
