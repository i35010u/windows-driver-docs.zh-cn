---
title: 高性能总线和适配器的设备状态
description: 高性能总线和适配器的设备状态
ms.assetid: 7a6b8048-d9aa-4169-aac5-150dc805f61b
keywords:
- Storport 驱动程序 WDK，错误
- 错误 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10dbf15b1c58d58ed773837b02d682966a02deeb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566203"
---
# <a name="device-status-for-high-performance-buses-and-adapters"></a>高性能总线和适配器的设备状态


## <span id="ddk_device_status_for_high_performance_buses_and_adapters_kg"></span><span id="DDK_DEVICE_STATUS_FOR_HIGH_PERFORMANCE_BUSES_AND_ADAPTERS_KG"></span>


Storport 驱动程序用于报告一些特定于传输的错误和 SCSI 端口驱动程序不会报告的条件。 例如，Storport 光纤通道，如"链接向下"错误，光纤通道主机总线适配器 (HBA) 之间的连接丢失或光纤通道 HBA 停止传输发出信号报告发生的错误情况。 Storport 支持光纤通道扩展链接服务，并能够报告已注册的状态更改通知 (Rscn) 和与光纤通道的循环初始化协议 (LIP) 相关联的错误。

 

 




