---
title: WDI_TLV_RTT
description: WDI_TLV_RTT 是一种 TLV，其中包含用于精确计时度量（INTERNAL.H）请求的测量往返时间（RTT），以 picoseconds。
ms.assetid: 82543997-30D3-469B-8EDE-31AF528BDDE4
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 65873dda02a98d87f3fca8318d5bff3111bcc1d6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918197"
---
# <a name="wdi_tlv_rtt"></a>WDI_TLV_RTT

**WDI_TLV_RTT**是一种 TLV，其中包含用于精确计时度量（internal.h）请求的测量往返时间（RTT），以 picoseconds。 

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15C

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
