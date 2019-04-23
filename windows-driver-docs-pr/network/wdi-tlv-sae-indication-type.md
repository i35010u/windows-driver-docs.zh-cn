---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE 是信息的包含继续 SAE 身份验证，目标是信息的 bssid 时或通知所需类型的身份验证的 TLV 无法继续。
ms.assetid: F505CA27-4B2F-4210-8BE4-F3B931B86DDC
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_INDICATION_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 92102685e65bb641b57d9db5ccdbeae1c4620420
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905323"
---
# <a name="wditlvsaeindicationtype"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE**是包含继续 SAE 身份验证，目标是 bssid 时或通知所需的信息类型的身份验证的 TLV 无法继续。

有效负载数据中使用此 TLV [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。

## <a name="tlv-type"></a>TLV 类型

0x14B

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_indication_type) | 继续使用目标 bssid 时，SAE 身份验证或通知所需的信息类型的身份验证无法继续。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
