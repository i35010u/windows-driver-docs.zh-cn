---
title: WDI_TLV_RTT_VARIANCE
description: WDI_TLV_RTT_VARIANCE 是包含用于计算往返时间 (RTT) 正常计时度量 (FTM) 在请求期间，如果使用多个度量值的度量值的统计方差 TLV。
ms.assetid: F8032726-4CC8-40F4-8FA1-840A3514A4B0
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT_VARIANCE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b19cf7aad3f6cc9c70f245628018679882458dc1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359089"
---
# <a name="wditlvrttvariance"></a>WDI_TLV_RTT_VARIANCE

**WDI_TLV_RTT_VARIANCE**是包含用于计算往返时间 (RTT) 正常计时度量 (FTM) 在请求期间，如果使用多个度量值的度量值的统计方差 TLV。 

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15E

## <a name="length"></a>长度

UINT64 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT64 | 用来计算 RTT 的度量值的方差。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
