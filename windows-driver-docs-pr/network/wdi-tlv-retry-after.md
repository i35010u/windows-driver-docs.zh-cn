---
title: WDI_TLV_RETRY_AFTER
description: WDI_TLV_RETRY_AFTER 是一种 TLV，其中包含持续时间（以秒为单位），在尝试请求目标 BSS (INTERNAL.H) 之前应经过的持续时间。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RETRY_AFTER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 39f9c202910c0bc76ebd71e43db1e902b61b6d1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834247"
---
# <a name="wdi_tlv_retry_after"></a>WDI_TLV_RETRY_AFTER

**WDI_TLV_RETRY_AFTER** 是一种 TLV，其中包含持续时间（以秒为单位），在尝试请求目标 BSS (internal.h) 之前应经过的持续时间。

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15A

## <a name="length"></a>长度

UINT16) 大小 (（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT16 | 尝试请求新的精细计时度量值之前应经过的持续时间（以秒为单位）， (从目标 BSS) 。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
