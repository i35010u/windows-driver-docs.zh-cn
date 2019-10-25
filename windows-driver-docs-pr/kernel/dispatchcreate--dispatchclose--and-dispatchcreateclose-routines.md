---
title: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
description: DispatchCreate、DispatchClose 和 DispatchCreateClose 例程
ms.assetid: 5c1c0036-71b1-4410-b157-f9ebe3b6ecfc
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8ba65849767383f5b4d0f66a4e0cb715a71c86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838734"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose 和 DispatchCreateClose 例程





驱动程序的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) irp，其中的 i/o 函数代码为[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)和[**IRP\_MJ 分别\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)。 此外，组合的[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程还可以处理这两个 i/o 函数代码的 irp。

Create 请求可能源自用户模式子系统，它尝试获取表示设备（可能代表应用程序或子系统级驱动程序）的文件对象的句柄，或从更高级别的驱动程序调用[**plxntb。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)或[**IoAttachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)。

互惠关闭请求源自与驱动程序的设备对象关联的文件对象句柄的用户模式子系统。

其中每个请求都是同步的。

 

 




