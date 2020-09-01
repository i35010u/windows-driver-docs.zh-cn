---
title: DispatchShutdown 例程
description: DispatchShutdown 例程
ms.assetid: e0d4ed56-a614-4dc8-9bb2-abfe38f05946
keywords:
- IRP_MJ_SHUTDOWN i/o 函数代码
- 调度例程 WDK 内核，DispatchShutdown 例程
- DispatchShutdown 例程
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d241945d13fb43c55a9319d1574775854be59c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189521"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown 例程





驱动程序的 [*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 关闭**](./irp-mj-shutdown.md) i/o 函数代码处理 irp。 具有数据的内部缓存的大容量存储设备的驱动程序必须处理此请求。 如果基础驱动程序维护数据的内部缓冲区，则还必须处理此请求，同时分层的大容量存储设备和中间驱动程序的驱动程序也必须处理此请求。

 

