---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS 是包含状态结果的位置配置信息 (LCI) 报表，TLV，如果其中一个请求期间正常计时度量 (FTM) 请求。
ms.assetid: 81122FDB-3E1C-472D-80D2-1C8F29F00D2D
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2fa629a2ef72b9e83df9e56f83b323644399b255
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365363"
---
# <a name="wditlvlcireportstatus"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS**是包含状态结果的位置配置信息 (LCI) 报表，TLV，如果一个请求期间正常计时度量 (FTM) 请求。

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15F

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI 报告的状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
