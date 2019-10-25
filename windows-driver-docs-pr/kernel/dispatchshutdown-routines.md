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
ms.openlocfilehash: dae881fdf0204d9bbc30410765be72b616b4df4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836825"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown 例程





驱动程序的[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程为[**irp\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)I/o 函数代码处理 irp。 具有数据的内部缓存的大容量存储设备的驱动程序必须处理此请求。 如果基础驱动程序维护数据的内部缓冲区，则还必须处理此请求，同时分层的大容量存储设备和中间驱动程序的驱动程序也必须处理此请求。

 

 




