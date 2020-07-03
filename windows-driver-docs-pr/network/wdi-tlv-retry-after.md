---
title: WDI_TLV_RETRY_AFTER
description: WDI_TLV_RETRY_AFTER 是一种 TLV，其中包含在尝试从目标 BSS 请求新的精细计时度量值（INTERNAL.H）之前应经过的持续时间（以秒为单位）。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RETRY_AFTER 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5d055b2fc04adb932c60c97f08a53e6ba33897ab
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917655"
---
# <a name="wdi_tlv_retry_after"></a>WDI_TLV_RETRY_AFTER

**WDI_TLV_RETRY_AFTER**是一种 TLV，其中包含在尝试从目标 BSS 请求新的精细计时度量值（internal.h）之前应经过的持续时间（以秒为单位）。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15A

## <a name="length"></a>长度

UINT16 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT16 | 尝试从目标 BSS 请求新的精细计时度量值（INTERNAL.H）之前应经过的持续时间（以秒为单位）。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
