---
title: WDI_TLV_SAE_FINITE_CYCLIC_GROUP
description: WDI_TLV_SAE_FINITE_CYCLIC_GROUP 是包含用于提交请求中同时进行身份验证的等于 (SAE) 身份验证的有限循环组 TLV。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_FINITE_CYCLIC_GROUP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 54002f71babf4c86ae05fb09a5899aa00910548b
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905276"
---
# <a name="wditlvsaefinitecyclicgroup"></a>WDI_TLV_SAE_FINITE_CYCLIC_GROUP

**WDI_TLV_SAE_FINITE_CYCLIC_GROUP**是包含用于提交请求中同时进行身份验证的等于 (SAE) 身份验证的有限循环组 TLV。

在中使用此 TLV [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x152

## <a name="length"></a>长度

UINT16 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT16 | 用于 SAE 身份验证的有限循环组。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
