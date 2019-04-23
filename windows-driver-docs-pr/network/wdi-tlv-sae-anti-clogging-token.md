---
title: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN
description: WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 是包含用于同时进行身份验证的等于 (SAE) 提交请求的防 clogging 令牌 TLV。
ms.assetid: 9A1046AE-029F-4B37-9523-655425BC93F1
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_ANTI_CLOGGING_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6628de1eb463dbc774fa513fe7688b2e2e08bdfa
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905344"
---
# <a name="wditlvsaeanticloggingtoken"></a>WDI_TLV_SAE_ANTI_CLOGGING_TOKEN

**WDI_TLV_SAE_ANTI_CLOGGING_TOKEN**是包含用于同时进行身份验证的等于 (SAE) 提交请求的防 clogging 令牌 TLV。

在中使用此 TLV [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x155

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | 防 clogging 标记。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
