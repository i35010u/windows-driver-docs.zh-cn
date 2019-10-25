---
title: 选择和取消选择连接到并行端口的 IEEE 1284 设备
description: 选择和取消选择连接到并行端口的 IEEE 1284 设备
ms.assetid: 1a3ac1b1-9180-4b71-8740-70c6fbe9a885
keywords:
- IEEE 1284 WDK
- 并行端口 WDK、IEEE 1284 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126866337ab2f7c159b27ad68a273242f36dd779
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842325"
---
# <a name="selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-port"></a>选择和取消选择连接到并行端口的 IEEE 1284 设备





客户端可以使用以下内部设备控制请求来选择和取消选择附加到并行端口的 IEEE 1284.3 设备：

[**IOCTL\_内部\_选择\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_select_device)

[**IOCTL\_内部\_取消选择\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_deselect_device)

内核模式驱动程序还可以使用系统提供的[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)，该例程是使用[**IOCTL\_内部\_获取\_并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)请求。 此请求返回一个[**并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_pnp_information)结构，其中包括指向系统提供的回调的以下指针：

-   **TrySelectDevice**成员是指向 PPARALLEL 的指针[ *\_尝试\_选择\_例程*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_select_routine)回拨，这会取消预选择 ieee 1284.3 菊花链设备或附加到并行端口的 ieee 1284 端链设备。

-   **DeselectDevice**成员是指向 PPARALLEL\_的指针，它可[*取消选择\_例程*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_deselect_routine)回拨，这将选择 ieee 1284.3 菊花链设备或连接到并行端口的 ieee 1284 端链设备。

Select 请求需要客户端的最低处理方式，因为系统提供的并行端口的函数驱动程序会将客户端的选择请求排队，前提是并行端口由另一个客户端分配。 并行端口函数驱动程序取消排队 select 请求后，它会尝试分配端口并选择 IEEE 1284.3 设备。 由于可接受的超时延迟或其他特定于设备的状态，客户端可以随时取消选择请求。

**请注意**   如果客户端仅使用[**PPARALLEL\_尝试\_选择 "\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_select_routine)回拨"，尝试选择并行设备，其他客户端正在对付并行端口，即系统提供的函数驱动程序对于并行端口，可能永远不会将端口分配给客户端。 若要确保成功，客户端必须使用[**IOCTL\_内部\_选择\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_select_device)请求。 （并行端口功能驱动程序将按接收选择设备请求的顺序，对端口分配请求和设备选择请求进行排队。）

 

当并行端口功能驱动程序为客户端选择 IEEE 1284.3 设备后，客户端将具有对端口和所选 IEEE 1284.3 设备的独占访问权限。 客户端必须调用[**PPARALLEL\_取消选择\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_deselect_routine)回拨，以释放端口并取消选择 IEEE 1284.3 设备。 客户端释放端口后，并行端口函数驱动程序取消排队挂起的请求（如果有），并处理请求。

Microsoft Windows 2000 支持每个端口四个菊花链设备;但是，Microsoft 建议每个端口最多使用两个菊花链设备。 Windows XP 每个端口最多支持两个菊花链设备。

 

 




