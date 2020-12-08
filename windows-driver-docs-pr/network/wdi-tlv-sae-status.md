---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS 是一种 TLV，其中包含等于 (SAE) 身份验证失败错误状态的同时身份验证。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 987f43c4528c1c65cd2a6a8686905a90cb92e139
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834213"
---
# <a name="wdi_tlv_sae_status"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS** 是一种 TLV，其中包含等于 (SAE) 身份验证失败错误状态的同时身份验证。

此 TLV 用于 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) 和 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中的命令参数。

## <a name="tlv-type"></a>TLV 类型

0x14C

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| [**WDI_SAE_STATUS**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) | SAE authentication 失败错误状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
