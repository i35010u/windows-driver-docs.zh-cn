---
title: DriverEntry 返回值
description: DriverEntry 返回值
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK 内核，返回值
- 返回值 WDK DriverEntry 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcad2c05ee3fb4deef9998fa9910557367bfd088
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403270"
---
# <a name="driverentry-return-values"></a>DriverEntry 返回值





[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程返回一个[NTSTATUS 值](using-ntstatus-values.md)，即状态 \_ 成功或适当的错误状态。

**DriverEntry**例程应将对[**IoRegisterDriverReinitialization**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)的任何调用推迟到返回状态成功之前 \_ 。 它不得进行此调用，除非它将返回状态 " \_ 成功"。

如果 **DriverEntry** 例程返回不是成功或信息性值的 NTSTATUS 值（如状态 \_ 成功），则不会加载该 **DriverEntry** 例程的驱动程序。

不能初始化的 **DriverEntry** 例程必须释放已在返回 control 之前设置的任何系统对象、系统资源和注册表资源。 如果驱动程序支持这些请求，则它应将 [**irp \_ mj \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md) 和 [**irp \_ mj \_ 关闭**](./irp-mj-shutdown.md) 的驱动程序对象中的调度入口点重置为 **NULL** 。

如果驱动程序无法初始化， **DriverEntry** 例程还应在返回 control 之前记录错误。 请参阅 [日志记录错误](logging-errors.md)。

请注意，如果驱动程序的[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程返回失败状态，则不会调用驱动程序的[*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程。

 

