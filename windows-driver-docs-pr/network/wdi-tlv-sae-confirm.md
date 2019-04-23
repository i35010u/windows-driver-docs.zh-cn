---
title: WDI_TLV_SAE_CONFIRM
description: WDI_TLV_SAE_CONFIRM 是包含同时进行身份验证的等于 (SAE) 确认请求的确认字段 TLV。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 949cf66d9025d3912bb347119af532ec0b9d152b
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905345"
---
# <a name="wditlvsaeconfirm"></a>WDI_TLV_SAE_CONFIRM

**WDI_TLV_SAE_CONFIRM**是包含同时进行身份验证的等于 (SAE) 确认请求的确认字段 TLV。

在中使用此 TLV [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x157

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | 确认字段中。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
