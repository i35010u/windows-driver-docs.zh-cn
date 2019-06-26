---
title: DriverEntry 返回值
description: DriverEntry 返回值
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK 内核，返回值
- 返回值 WDK DriverEntry 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 665bc0aa9c21bf9bfc199e914ef91e3365410d3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384956"
---
# <a name="driverentry-return-values"></a>DriverEntry 返回值





一个[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程返回[NTSTATUS 值](ntstatus-values.md)，任一状态\_成功或相应的错误状态。

**DriverEntry**例程应推迟到任何调用[ **IoRegisterDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization)直到只返回状态前\_成功。 它必须进行此调用，除非它将返回状态\_成功。

如果**DriverEntry**例程将返回未成功完成的 NTSTATUS 值或信息性的值，如状态\_成功后，该驱动程序**DriverEntry**例程不会加载。

一个**DriverEntry**将失败，初始化的例程必须释放任何系统对象、 系统资源和它已设置为之前会将控件返回的注册表资源。 它应重置的驱动程序对象中的驱动程序的调度入口点[ **IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)并[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)到**NULL**如果驱动程序支持这些请求。

如果驱动程序将失败初始化**DriverEntry**例程还应记录错误返回控件之前。 请参阅[日志记录错误](logging-errors.md)。

请注意，驱动程序的[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)如果驱动程序不调用例程[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程将返回失败状态。

 

 




