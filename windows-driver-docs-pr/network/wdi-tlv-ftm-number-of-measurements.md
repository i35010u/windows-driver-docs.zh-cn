---
title: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
description: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 是一种 TLV，其中包含用于提供精确计时度量值的往返时间 (RTT)  (INTERNAL.H) 请求。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 502e34e169942f39b95d7e53bfd72d8054d9c9af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825365"
---
# <a name="wdi_tlv_ftm_number_of_measurements"></a>WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS

**WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS** 是一种 TLV，其中包含用于提供精确计时度量值的往返时间 (RTT)  (internal.h) 请求。

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15B

## <a name="length"></a>长度

UINT16) 大小 (（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT16 | 用于提供 RTT 的度量值的数量。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
