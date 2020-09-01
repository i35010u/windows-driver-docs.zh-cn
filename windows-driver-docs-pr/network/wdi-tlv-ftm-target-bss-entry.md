---
title: WDI_TLV_FTM_TARGET_BSS_ENTRY
description: WDI_TLV_FTM_TARGET_BSS_ENTRY 是一种 TLV，其中包含用于精确计时度量的 BSS 目标的信息 (应完成的 INTERNAL.H) 过程。
ms.assetid: 04C996C7-8207-4363-A990-5CF39B0333F8
ms.date: 02/13/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_TARGET_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6f9a8ed5945ab128cfb981b727352af6e997da2d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213714"
---
# <a name="wdi_tlv_ftm_target_bss_entry"></a>WDI_TLV_FTM_TARGET_BSS_ENTRY

**WDI_TLV_FTM_TARGET_BSS_ENTRY** 是一种 TLV，其中包含用于精确计时度量的 BSS 目标的信息 (应完成的 internal.h) 过程。 

此 TLV 用于 [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)的任务参数。

## <a name="tlv-type"></a>TLV 类型

0x162

## <a name="length"></a>Length

Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值

| TLV | 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | 目标 BSS 的 BSSID。 |
| [WDI_TLV_PROBE_RESPONSE_FRAME](wdi-tlv-probe-response-frame.md) | TLV\<LIST\<UINT8>> |   | X | 探测响应帧。 如果未收到探测响应，则此字段为空。 |
| [WDI_TLV_BEACON_FRAME](wdi-tlv-beacon-frame.md) | TLV\<LIST\<UINT8>> |   | X | 信号框架。 如果未收到任何信号，则此字段为空。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | 收到的信号强度指示器 (对等方发出的信号或探测响应的 RSSI) 值。 此单位为1.0 毫瓦 (dBm) 的分贝。 |
|  | UINT32 |   |   | 链接质量值介于0到100之间。 值100指定最高的链接质量。 |
| [WDI_TLV_BSS_ENTRY_CHANNEL_INFO](wdi-tlv-bss-entry-channel-info.md) | UINT32 |   |   | 目标 BSS 的逻辑通道号。 |
|   | UINT32 |   |   | 目标 BSS 的带区 ID。 |
| [WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT](wdi-tlv-bss-entry-device-context.md) | TLV\<LIST\<UINT8>> |  |  | IHV 组件提供的关于此对等方的上下文数据。 这可以是用于存储 IHV 组件要维护的每个 BSS 输入状态的美元。 为了避免生存期管理问题，IHV 组件不能在此字段中使用指针。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | UINT8 |   |   | 可能的值： <ul><li>0：不需要 LCI 报表。</li><li>1：应请求 LCI 报告。</li></ul> |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp