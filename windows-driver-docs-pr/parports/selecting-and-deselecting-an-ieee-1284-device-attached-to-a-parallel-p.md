---
title: 选择和取消选择连接到并行端口的 IEEE 1284 设备
description: 选择和取消选择连接到并行端口的 IEEE 1284 设备
ms.assetid: 1a3ac1b1-9180-4b71-8740-70c6fbe9a885
keywords:
- IEEE 1284 WDK
- 并行端口 WDK，IEEE 1284 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b461a9a30a53bb1fb6be264a94f397d9c2ad461
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358485"
---
# <a name="selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-port"></a>选择和取消选择连接到并行端口的 IEEE 1284 设备





客户端可以选择或取消选择通过使用以下内置设备控制请求附加到并行端口的 IEEE 1284.3 设备：

[**IOCTL\_INTERNAL\_SELECT\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_select_device)

[**IOCTL\_INTERNAL\_DESELECT\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_deselect_device)

内核模式驱动程序还可以使用系统提供[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)通过使用获得[ **IOCTL\_内部\_获取\_并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)请求。 此请求将返回[**并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parallel_pnp_information)结构，它包括以下指向系统提供的回调：

-   **TrySelectDevice**成员是指向[ *PPARALLEL\_尝试\_选择\_例程*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_try_select_routine)回调，取消选择IEEE 1284.3 菊花链设备或连接到并行端口的 IEEE 1284 链结束设备。

-   **DeselectDevice**成员是指向[ *PPARALLEL\_取消选择\_例程*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_deselect_routine)回调，后者选择 IEEE 1284.3 菊花链设备或连接到并行端口的 IEEE 1284 链结束设备。

选择请求需要最少处理的客户端，因为并行端口的系统提供的函数驱动程序对请求进行排队选择客户端如果并行端口分配的另一个客户端。 并行端口功能驱动程序通过选择请求取消排队后，它将尝试分配端口并选择 IEEE 1284.3 设备。 由于可接受超时延迟或某些其他特定于设备的条件，客户端可以在任何时候取消选择请求。

**请注意**  如果客户端仅使用[ **PPARALLEL\_尝试\_选择\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_try_select_routine)回调以尝试选择并行系统提供的函数驱动程序的并行端口设备和其他客户端在争用的并行端口，可能永远不会分配多端口到客户端。 若要确保成功，客户端必须使用[ **IOCTL\_内部\_选择\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_select_device)请求。 （并行端口函数驱动程序队列和随后的进程，端口分配的请求和设备的选择的设备中收到的请求的顺序选择请求）。

 

并行端口功能驱动程序的客户端选择 IEEE 1284.3 设备后，客户端具有独占访问权限的端口和所选的 IEEE 1284.3 设备。 客户端必须调用[ **PPARALLEL\_取消选择\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_deselect_routine)回调以释放该端口，并取消选择 IEEE 1284.3 设备。 客户端释放该端口后，并行端口功能驱动程序取消排队的挂起的请求，如果有，并处理请求。

Microsoft Windows 2000 支持每个端口; 的四个菊花链设备但是，Microsoft 建议使用最多两个菊花链设备每个端口。 Windows XP 支持最多两个菊花链每个设备端口。

 

 




