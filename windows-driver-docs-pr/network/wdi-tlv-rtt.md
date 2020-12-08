---
title: WDI_TLV_RTT
description: WDI_TLV_RTT 是一种 TLV，其中包含在 picoseconds 中 (RTT) 的测量往返时间，用于精确计时度量值 (INTERNAL.H) 请求。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cad21833f196f045259559bc1254c0a1955c07d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818011"
---
# <a name="wdi_tlv_rtt"></a>WDI_TLV_RTT

**WDI_TLV_RTT** 是一种 TLV，其中包含在 picoseconds 中 (RTT) 的测量往返时间，用于精确计时度量值 (internal.h) 请求。 

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15C

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
