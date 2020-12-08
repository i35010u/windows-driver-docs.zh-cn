---
title: 高性能总线和适配器的设备状态
description: 高性能总线和适配器的设备状态
keywords:
- Storport 驱动程序 WDK，错误
- 错误 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed39d3c31dd4bf71b8b510026fabd6ac1abc4899
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804681"
---
# <a name="device-status-for-high-performance-buses-and-adapters"></a>高性能总线和适配器的设备状态


## <span id="ddk_device_status_for_high_performance_buses_and_adapters_kg"></span><span id="DDK_DEVICE_STATUS_FOR_HIGH_PERFORMANCE_BUSES_AND_ADAPTERS_KG"></span>


Storport 驱动程序设计用于报告某些传输特定的错误和 SCSI 端口驱动程序未报告的情况。 例如，Storport 报告在光纤通道上出现的错误条件，如 "链路关闭" 错误，其中光纤通道主机总线适配器 (HBA) 之间的连接丢失或光纤通道 HBA 停止传输信号。 Storport 支持光纤通道的扩展链接服务，并能够报告注册的状态更改通知 (与光纤通道的循环初始化协议关联的) 和错误 (LIP) 。

 

 




