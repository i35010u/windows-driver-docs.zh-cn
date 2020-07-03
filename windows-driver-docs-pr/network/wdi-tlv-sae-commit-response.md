---
title: WDI_TLV_SAE_COMMIT_RESPONSE
description: WDI_TLV_SAE_COMMIT_RESPONSE 是一种 TLV，其中包含 Equals （SAE）提交响应帧的同时身份验证。
ms.assetid: 3E243737-F1C8-4554-96D2-E05C77DBA8B6
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_COMMIT_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7572824c416f8c687af9dbece137135b2063ff48
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918193"
---
# <a name="wdi_tlv_sae_commit_response"></a>WDI_TLV_SAE_COMMIT_RESPONSE

**WDI_TLV_SAE_COMMIT_RESPONSE**是一种 TLV，其中包含 EQUALS （SAE）提交响应帧的同时身份验证。

此 TLV 在[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中使用。

## <a name="tlv-type"></a>TLV 类型

0x14D

## <a name="length"></a>长度

UINT8 元素数组的大小（以字节为单位）。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT8 [] | SAE 提交响应帧。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
