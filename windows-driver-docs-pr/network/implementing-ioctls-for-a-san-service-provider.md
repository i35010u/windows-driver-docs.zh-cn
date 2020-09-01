---
title: 实现 SAN 服务提供程序的 IOCTL
description: 实现 SAN 服务提供程序的 IOCTL
ms.assetid: 7d4c7039-6b42-4620-aee5-9189b4acd030
keywords:
- 代理驱动程序 WDK San，IOCTLs
- SAN 代理驱动程序 WDK，IOCTLs
- IOCTLs WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c640b504239aec08c4137c496097de981d99d9e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217622"
---
# <a name="implementing-ioctls-for-a-san-service-provider"></a>实现 SAN 服务提供程序的 IOCTL





如果 SAN 服务提供程序将 (IOCTL) 请求发送到代理驱动程序，则驱动程序应实施 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 调度例程来处理这些请求。 IOCTL 请求可以是检索分配给驱动程序的 Nic 的 IP 地址列表的请求，或者请求分配或释放内存的请求。 **DriverEntry**例程必须指定调度例程的入口点。

代理驱动程序的设备控制例程将调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) 函数，在此函数中，设备控制例程会将指向传递到该例程的 IRP 传递到该函数。 然后，设备控制例程会确定接收了哪些 IOCTL 请求并相应地处理请求。

当前 IOCTL 请求完成后，设备控制例程将调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 函数并传递操作的状态。 此状态将返回到 SAN 服务提供商。

 

