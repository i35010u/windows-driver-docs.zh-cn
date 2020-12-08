---
title: WDI_TLV_SAE_CONFIRM
description: WDI_TLV_SAE_CONFIRM 是一种 TLV，其中包含对等 (SAE) 确认请求进行同时身份验证的确认字段。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_CONFIRM 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 83aafcafba2a793c6414d349cf8965ac022d7ea2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817991"
---
# <a name="wdi_tlv_sae_confirm"></a>WDI_TLV_SAE_CONFIRM

**WDI_TLV_SAE_CONFIRM** 是一种 TLV，其中包含对等 (SAE) 确认请求进行同时身份验证的确认字段。

此 TLV 用于 [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)。

## <a name="tlv-type"></a>TLV 类型

0x157

## <a name="length"></a>长度

UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT8 [] | 确认字段。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
