---
title: WDI_TLV_SAE_ELEMENT
description: WDI_TLV_SAE_ELEMENT 是 TLV 包含编码字段元素 (EFE) 同时进行身份验证的等于 (SAE) 提交请求。
ms.assetid: B5E4DC7A-40B5-4F1D-A1C5-D2526FA0DF4D
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_ELEMENT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 47bca20236a58cd367c28f87a947d54eeed7b123
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905294"
---
# <a name="wditlvsaeelement"></a>WDI_TLV_SAE_ELEMENT

**WDI_TLV_SAE_ELEMENT**是 TLV 包含编码字段元素 (EFE) 同时进行身份验证的等于 (SAE) 提交请求。

在中使用此 TLV [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x154

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | EFE 的一部分。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
