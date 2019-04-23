---
title: WDI_TLV_FTM_RESPONSE
description: WDI_TLV_FTM_RESPONSE 是包含 BSS 目标正常计时度量 (FTM) 响应信息 TLV。
ms.assetid: 7FD63544-F7FF-4593-A525-A6BEA2A56BB7
ms.date: 02/13/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d2b4ba9140eb8577e76af1f48bfcc458f04ebe6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905223"
---
# <a name="wditlvftmresponse"></a>WDI_TLV_FTM_RESPONSE

**WDI_TLV_FTM_RESPONSE**是包含 BSS 目标正常计时度量 (FTM) 响应信息 TLV。 

有效负载数据中使用此 TLV [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)任务完成的指示。

## <a name="tlv-type"></a>TLV 类型

0x163

## <a name="length"></a>长度

所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |   | 目标属于此 FTM 响应的 BSSID。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ftm_response_status) |  |   | FTM 响应状态。 如果成功，此 TLV 中的字段的其余部分都存在。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md)| UINT16 |  |  | 一个时间段，以秒为单位，尝试请求新 FTM 来自此目标之前应经过。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | UINT16 |  |   | 使用提供的往返行程时间 (RTT) 的度量值数。 如果 FTM 响应状态表示成功，则此字段是必填项。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | 接收到的信号强度指示符 (RSSI) 从 FTM 目标。 这是到 1.0 毫瓦 (dBm) 引用的分贝为单位。 如果 FTM 响应状态表示成功，则此字段是必填项。 |
| 与上面的行相同  | UINT32 |   |   | 链接质量 FTM 目标，范围从 0 到 100 之间的值。 100 的值指定最高的链接质量。 如果 FTM 响应状态表示成功，则此字段是必填项。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | UINT32 |   |   | Picoseconds 测量的往返时间 (RTT)。 如果 FTM 响应状态表示成功，则此字段是必填项。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | UINT32 |   |   | 准确性或预期的程度，为 true 的值提供的 RTT 度量程度。 单位为 picoseconds 中。 有关详细信息，请参阅[WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md)。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | UINT64 |   |   | 如果使用了多个度量来计算 RTT，此字段提供了使用的度量值的统计方差。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_lci_report_status) |   |   | 如果请求了 LCI 报告，此字段提供了状态结果。 如果成功，则以下字段是存在并且是强制性。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | TLV\<LIST\<UINT8>> |   |   | 位置配置信息 (LCI) 定义的报表，在部分 9.4.2.22.10 [802-11-2016年标准](https://standards.ieee.org/standard/802_11-2016.html)，包括 LCI 子元素和其他可用的可选子元素。 换而言之，这是度量报表元素的度量报表部分 (根据从部分 9.4.2.22 [802-11-2016年标准](https://standards.ieee.org/standard/802_11-2016.html))。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
