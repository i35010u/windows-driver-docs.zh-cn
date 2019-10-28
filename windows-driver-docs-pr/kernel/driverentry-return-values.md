---
title: DriverEntry 返回值
description: DriverEntry 返回值
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK 内核，返回值
- 返回值 WDK DriverEntry 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9e930aa1f57e47e53a904945748d4110bc673e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838718"
---
# <a name="driverentry-return-values"></a>DriverEntry 返回值





[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程返回一个[NTSTATUS 值](ntstatus-values.md)，状态\_成功或适当的错误状态。

**DriverEntry**例程应延迟对[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)的任何调用，直到其返回状态\_SUCCESS。 除非它将返回状态\_成功，否则不能进行此调用。

如果**DriverEntry**例程返回的 NTSTATUS 值不是 success 或信息性值（如 STATUS\_success），则不会加载该**DriverEntry**例程的驱动程序。

不能初始化的**DriverEntry**例程必须释放已在返回 control 之前设置的任何系统对象、系统资源和注册表资源。 如果驱动程序支持这些**请求，则**它应将 IRP 的驱动程序对象中的调度入口点重置为[**IRP\_MJ\_FLUSH\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)和[**IRP\_MJ\_SHUTDOWN**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown) 。

如果驱动程序无法初始化， **DriverEntry**例程还应在返回 control 之前记录错误。 请参阅[日志记录错误](logging-errors.md)。

请注意，如果驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程返回失败状态，则不会调用驱动程序的[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。

 

 




