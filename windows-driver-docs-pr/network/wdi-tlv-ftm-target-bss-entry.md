---
title: WDI_TLV_FTM_TARGET_BSS_ENTRY
description: WDI_TLV_FTM_TARGET_BSS_ENTRY 是 TLV 包含 BSS 目标应与其完成正常计时度量 (FTM) 过程的信息。
ms.assetid: 04C996C7-8207-4363-A990-5CF39B0333F8
ms.date: 02/13/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_TARGET_BSS_ENTRY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 695c46e35e34d38083b4c95cedecfff1026ed6d6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905250"
---
# <a name="wditlvftmtargetbssentry"></a>WDI_TLV_FTM_TARGET_BSS_ENTRY

**WDI_TLV_FTM_TARGET_BSS_ENTRY**是 TLV 包含 BSS 目标使用的正常时间度量 (FTM) 的情况下应完成过程的信息。 

中的任务参数使用此 TLV [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)。

## <a name="tlv-type"></a>TLV 类型

0x162

## <a name="length"></a>长度

所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | 目标 BSS BSSID。 |
| [WDI_TLV_PROBE_RESPONSE_FRAME](wdi-tlv-probe-response-frame.md) | TLV\<LIST\<UINT8>> |   | X | 探测响应帧。 如果不收到任何探测响应，此字段为空。 |
| [WDI_TLV_BEACON_FRAME](wdi-tlv-beacon-frame.md) | TLV\<LIST\<UINT8>> |   | X | 信号帧。 如果收到没有信号，则此字段为空。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | 接收到的信号强度指示 (RSSI) 符信号或探测响应从对等方的值。 这是到 1.0 毫瓦 (dBm) 引用的分贝为单位。 |
|  | UINT32 |   |   | 链接质量值范围从 0 到 100 之间。 100 的值指定最高的链接质量。 |
| [WDI_TLV_BSS_ENTRY_CHANNEL_INFO](wdi-tlv-bss-entry-channel-info.md) | UINT32 |   |   | 目标 BSS 逻辑通道数。 |
|   | UINT32 |   |   | 目标 BSS 外 ID。 |
| [WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT](wdi-tlv-bss-entry-device-context.md) | TLV\<LIST\<UINT8>> |  |  | 有关此对等方 IHV 提供组件的上下文数据。 这可以是用于存储 IHV 组件想要维护的每个 BSS 入口状态。 若要避免生存期管理问题，IHV 组件必须在此字段中不使用指针。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | UINT8 |   |   | 可能值： <ul><li>0:不需要 LCI 报表。</li><li>1：应请求 LCI 报表。</li></ul> |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
