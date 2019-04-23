---
title: WDI_TLV_SAE_COMMIT_RESPONSE
description: WDI_TLV_SAE_COMMIT_RESPONSE 是包含同时进行身份验证的等于 (SAE) 提交响应帧 TLV。
ms.assetid: 3E243737-F1C8-4554-96D2-E05C77DBA8B6
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_COMMIT_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 05b4bebba6d720897e59f77414a90421cc233484
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905309"
---
# <a name="wditlvsaecommitresponse"></a>WDI_TLV_SAE_COMMIT_RESPONSE

**WDI_TLV_SAE_COMMIT_RESPONSE**是包含同时进行身份验证的等于 (SAE) 提交响应帧 TLV。

有效负载数据中使用此 TLV [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。

## <a name="tlv-type"></a>TLV 类型

0x14D

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | SAE 提交响应帧。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
