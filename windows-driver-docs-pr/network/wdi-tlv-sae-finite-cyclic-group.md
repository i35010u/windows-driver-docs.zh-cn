---
title: WDI_TLV_SAE_FINITE_CYCLIC_GROUP
description: WDI_TLV_SAE_FINITE_CYCLIC_GROUP 是一种 TLV，其中包含提交请求中使用的有限循环组，用于同时对等于 (SAE) 身份验证进行身份验证。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_FINITE_CYCLIC_GROUP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 80515fe85c20bb99097057ef017a41184e00f657
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834210"
---
# <a name="wdi_tlv_sae_finite_cyclic_group"></a>WDI_TLV_SAE_FINITE_CYCLIC_GROUP

**WDI_TLV_SAE_FINITE_CYCLIC_GROUP** 是一种 TLV，其中包含提交请求中使用的有限循环组，用于同时对等于 (SAE) 身份验证进行身份验证。

此 TLV 用于 [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x152

## <a name="length"></a>长度

UINT16) 大小 (（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT16 | 用于 SAE authentication 的有限循环组。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
