---
title: DriverEntry 返回值
description: DriverEntry 返回值
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK 内核，返回值
- 返回值 WDK DriverEntry 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb670ddabd19032ab68d5d5ce1d0939632e53264
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359471"
---
# <a name="driverentry-return-values"></a>DriverEntry 返回值





一个[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程返回[NTSTATUS 值](ntstatus-values.md)，任一状态\_成功或相应的错误状态。

**DriverEntry**例程应推迟到任何调用[ **IoRegisterDriverReinitialization** ](https://msdn.microsoft.com/library/windows/hardware/ff549511)直到只返回状态前\_成功。 它必须进行此调用，除非它将返回状态\_成功。

如果**DriverEntry**例程将返回未成功完成的 NTSTATUS 值或信息性的值，如状态\_成功后，该驱动程序**DriverEntry**例程不会加载。

一个**DriverEntry**将失败，初始化的例程必须释放任何系统对象、 系统资源和它已设置为之前会将控件返回的注册表资源。 它应重置的驱动程序对象中的驱动程序的调度入口点[ **IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff550760)并[ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550807)到**NULL**如果驱动程序支持这些请求。

如果驱动程序将失败初始化**DriverEntry**例程还应记录错误返回控件之前。 请参阅[日志记录错误](logging-errors.md)。

请注意，驱动程序的[ *Unload* ](https://msdn.microsoft.com/library/windows/hardware/ff564886)如果驱动程序不调用例程[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程将返回失败状态。

 

 




