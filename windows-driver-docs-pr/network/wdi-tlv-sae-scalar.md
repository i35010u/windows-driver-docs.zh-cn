---
title: WDI_TLV_SAE_SCALAR
description: WDI_TLV_SAE_SCALAR 是包含同时进行身份验证的等于 (SAE) 提交请求有限字段元素 (FFE) TLV。
ms.assetid: 23B8B2DB-D451-4E8D-B8A3-D66A81DF599C
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_SCALAR 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a83799cb55108cf95583122f280ac0cf188841d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359033"
---
# <a name="wditlvsaescalar"></a>WDI_TLV_SAE_SCALAR

**WDI_TLV_SAE_SCALAR**是包含同时进行身份验证的等于 (SAE) 提交请求有限字段元素 (FFE) TLV。

在中使用此 TLV [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x153

## <a name="length"></a>长度

UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT8[] | FFE。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
