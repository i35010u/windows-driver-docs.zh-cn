---
title: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS
description: WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 是一种 TLV，其中包含用于提供精确计时度量值（INTERNAL.H）请求的往返时间（RTT）的度量值数。
ms.assetid: C629B5F5-FB30-4808-A392-69150C5A2FA3
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7c53d4881f59ac0c13895b9f0578b34e9e02eeac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916146"
---
# <a name="wdi_tlv_ftm_number_of_measurements"></a>WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS

**WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS**是一种 TLV，其中包含用于提供精确计时度量值（internal.h）请求的往返时间（RTT）的度量值数。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15B

## <a name="length"></a>长度

UINT16 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT16 | 用于提供 RTT 的度量值的数量。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
