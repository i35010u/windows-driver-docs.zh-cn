---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS 是一个 TLV，其中包含位置配置信息（LCI）报告的状态结果（如果在精细计时度量（INTERNAL.H）请求期间请求了一个）。
ms.assetid: 81122FDB-3E1C-472D-80D2-1C8F29F00D2D
ms.date: 02/15/2019
keywords:
- WDI_TLV_LCI_REPORT_STATUS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3cb1de7eee21584249374048c7d6a1f0362bf922
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842467"
---
# <a name="wdi_tlv_lci_report_status"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS**是一个 TLV，其中包含位置配置信息（LCI）报告的状态结果（如果在精细计时度量（internal.h）请求期间请求了一个）。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)中。

## <a name="tlv-type"></a>TLV 类型

0x15F

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI 报表的状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
