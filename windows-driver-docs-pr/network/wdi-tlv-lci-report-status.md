---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS 是一种 TLV，其中包含位置配置信息（LCI）报表的状态结果（如果在精细计时度量（INTERNAL.H）请求期间请求了此项）。
ms.assetid: 81122FDB-3E1C-472D-80D2-1C8F29F00D2D
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2b3a3fe0f60e6a550413b5e4c855eeea811d1584
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916768"
---
# <a name="wdi_tlv_lci_report_status"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS**是一种 TLV，其中包含位置配置信息（LCI）报表的状态结果（如果在精细计时度量（internal.h）请求期间请求了此项）。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15F

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI 报表的状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
