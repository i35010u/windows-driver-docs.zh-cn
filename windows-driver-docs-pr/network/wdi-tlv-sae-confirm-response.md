---
title: WDI_TLV_SAE_COMMIT_RESPONSE
description: WDI_TLV_SAE_CONFIRM_RESPONSE 是包含同时进行身份验证的等于 (SAE) 确认响应帧 TLV。
ms.assetid: 42ACD823-3FFB-442F-B81C-82446C3606FF
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 994ffc57f0550dc5ec59e7ae9f1f262d4e2f64ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359340"
---
# <a name="wditlvsaeconfirmresponse"></a>WDI_TLV_SAE_COMMIT_RESPONSE

**WDI_TLV_SAE_CONFIRM_RESPONSE**是包含同时进行身份验证的等于 (SAE) 确认响应帧 TLV。

有效负载数据中使用此 TLV [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。

## <a name="tlv-type"></a>TLV 类型

0x14E

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | SAE 确认响应帧。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
