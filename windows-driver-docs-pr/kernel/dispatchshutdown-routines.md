---
title: DispatchShutdown 例程
description: DispatchShutdown 例程
ms.assetid: e0d4ed56-a614-4dc8-9bb2-abfe38f05946
keywords:
- IRP_MJ_SHUTDOWN I/O 函数代码
- 调度例程 WDK 内核，DispatchShutdown 例程
- DispatchShutdown 例程
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f93fd8a4c832dd88ead14d9ffdd82d44e0556f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384968"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown 例程





驱动程序的[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown) I/O函数代码。 具有内部缓存中的对数据的大容量存储设备的驱动程序必须处理此请求。 大容量存储设备的驱动程序和它们的上层的中间驱动程序还如果基础驱动程序维护的数据的内部缓冲区必须处理此请求。

 

 




