---
title: WDI_TLV_RTT
description: WDI_TLV_RTT 是包含的测量的往返时间 (RTT) 中 picoseconds，没问题计时度量 (FTM) 请求 TLV。
ms.assetid: 82543997-30D3-469B-8EDE-31AF528BDDE4
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4584bfefa92829d249502e4ebf11816ef06a6390
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359190"
---
# <a name="wditlvrtt"></a>WDI_TLV_RTT

**WDI_TLV_RTT**包含测量的往返时间 (RTT) TLV 处于 picoseconds，没问题计时度量 (FTM) 请求。 

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15C

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
