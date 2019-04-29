---
title: 实现 SAN 服务提供程序的 IOCTL
description: 实现 SAN 服务提供程序的 IOCTL
ms.assetid: 7d4c7039-6b42-4620-aee5-9189b4acd030
keywords:
- 代理驱动程序 WDK San Ioctl
- SAN 代理驱动程序 WDK Ioctl
- Ioctl WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a831bf17ff3870e44bf7f43bdfb368c854f3260a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362949"
---
# <a name="implementing-ioctls-for-a-san-service-provider"></a>实现 SAN 服务提供程序的 IOCTL





如果 SAN 服务提供商 I/O 控制 (IOCTL) 将请求发送给代理驱动程序，该驱动程序应实现[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)调度若要处理这些请求的例程。 IOCTL 请求可以检索分配给驱动程序的 Nic 的 IP 地址的列表的请求或请求分配或释放内存。 **DriverEntry**例程必须指定的调度例程的入口点。

代理驱动程序的设备控制例程调用[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)函数，设备控制例程将指针传递到 IRP 传递给例程。 然后，设备控制例程确定接收哪些 IOCTL 请求，并相应地处理请求。

当前 IOCTL 请求完成之后，设备控制例程调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)函数并传递操作的状态。 SAN 服务提供程序返回此状态。

 

 





