---
title: WDI_TLV_FTM_RESPONSE
description: WDI_TLV_FTM_RESPONSE 是一个 TLV，其中包含来自 BSS 目标的精细计时度量（INTERNAL.H）响应信息。
ms.assetid: 7FD63544-F7FF-4593-A525-A6BEA2A56BB7
ms.date: 02/13/2019
keywords:
- WDI_TLV_FTM_RESPONSE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8b980333af5f8568c171bde94a7e0284ca4eaf53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844986"
---
# <a name="wdi_tlv_ftm_response"></a>WDI_TLV_FTM_RESPONSE

**WDI_TLV_FTM_RESPONSE**是一个 TLV，其中包含来自 BSS 目标的精细计时度量（internal.h）响应信息。 

此 TLV 用于[NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)任务完成指示的负载数据。

## <a name="tlv-type"></a>TLV 类型

0x163

## <a name="length"></a>长度

所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |   | 此 INTERNAL.H 响应所属目标的 BSSID。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) |  |   | INTERNAL.H 响应状态。 如果成功，则会出现此 TLV 中的其余字段。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md)| UINT16 |  |  | 尝试从该目标请求新 INTERNAL.H 之前应经过的持续时间（以秒为单位）。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | UINT16 |  |   | 用于提供往返时间（RTT）的度量值的数量。 如果 INTERNAL.H 响应状态为 "成功"，则此字段是必需的。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | 从 INTERNAL.H 目标接收的信号强度指示器（RSSI）。 这是指1.0 毫瓦（dBm）的分贝单位。 如果 INTERNAL.H 响应状态为 "成功"，则此字段是必需的。 |
| 与上一行相同  | UINT32 |   |   | INTERNAL.H 目标的链接质量值，范围从0到100。 值100指定最高的链接质量。 如果 INTERNAL.H 响应状态为 "成功"，则此字段是必需的。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | UINT32 |   |   | Picoseconds 中测量的往返时间（RTT）。 如果 INTERNAL.H 响应状态为 "成功"，则此字段是必需的。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | UINT32 |   |   | 所提供的 RTT 度量值为 true 值的准确性或预期的靠近程度程度。 单元位于 picoseconds 中。 有关详细信息，请参阅[WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md)。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | UINT64 |   |   | 如果使用多个度量值计算 RTT，此字段将提供所用度量值的统计方差。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) |   |   | 如果请求 LCI 报表，此字段将提供状态结果。 如果成功，则以下字段存在并且是必需的。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | TLV\<LIST\<UINT8 > > |   |   | "位置配置信息" （LCI）报表，在[802-11-2016 标准](https://standards.ieee.org/standard/802_11-2016.html)的 "9.4.2.22.10" 部分中定义，包括 LCI 子元素和其他可用的可选子元素。 换句话说，这是度量报表元素的度量报表部分（从[802-11-2016 标准](https://standards.ieee.org/standard/802_11-2016.html)的9.4.2.22 节开始）。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
