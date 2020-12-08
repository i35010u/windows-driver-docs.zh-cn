---
title: DispatchShutdown 例程
description: DispatchShutdown 例程
keywords:
- IRP_MJ_SHUTDOWN i/o 函数代码
- 调度例程 WDK 内核，DispatchShutdown 例程
- DispatchShutdown 例程
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e64583726c00e9f43736c99875fa10cdd50cb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833437"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown 例程





驱动程序的 [*DispatchShutdown*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 关闭**](./irp-mj-shutdown.md) i/o 函数代码处理 irp。 具有数据的内部缓存的大容量存储设备的驱动程序必须处理此请求。 如果基础驱动程序维护数据的内部缓冲区，则还必须处理此请求，同时分层的大容量存储设备和中间驱动程序的驱动程序也必须处理此请求。

 

