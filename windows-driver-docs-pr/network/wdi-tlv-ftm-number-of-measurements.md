---
title: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
description: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 是包含用于提供好计时度量 (FTM) 请求的往返行程时间 (RTT) 的度量数 TLV。
ms.assetid: C629B5F5-FB30-4808-A392-69150C5A2FA3
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8ddb6d6a3db8d8d4755818084004f073d695b720
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382888"
---
# <a name="wditlvftmnumberofmeasurements"></a>WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS

**WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS**是包含的度量值用于提供往返时间 (RTT) 号的正常时间度量 (FTM) 请求 TLV。

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15B

## <a name="length"></a>长度

UINT16 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT16 | 用于提供 RTT 测量数量。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
