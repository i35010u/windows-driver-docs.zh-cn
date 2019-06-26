---
title: 设置和清除并行设备的通信模式
description: 设置和清除并行设备的通信模式
ms.assetid: 2ff53ed0-dbb7-4c8f-b6e4-5f7d20124a7c
keywords:
- 并行设备 WDK、 通信模式
- 通信模式 WDK 并行设备
- 清除通信模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda0a990fd77a8309fc93129db92dd54ba1e5a0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358478"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>设置和清除并行设备的通信模式





客户端可以设置使用以下设备控制请求的并行设备的通信模式：

-   [**IOCTL\_IEEE1284\_获取\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)返回当前在设备上设置的通信协议。 端口没有要锁定用于此请求。

-   [**IOCTL\_IEEE1284\_NEGOTIATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)协商新的通信模式。 必须分配的并行端口并选择 IEEE 1284.3 设备。

-   [**IOCTL\_内部\_断开连接\_空闲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_disconnect_idle)通信模式设置为 IEEE\_兼容。 必须分配的并行端口并选择 IEEE 1284.3 设备。

内核模式驱动程序还可以使用系统提供[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parclass_connect)请求将返回[ **PARCLASS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parclass_information)结构，其中包含以下系统提供的回调例程的指针：

-   **DetermineIeeeMode**成员是指向[ **PDETERMINE\_IEEE\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pdetermine_ieee_modes)回调，它确定 IEEE 通信并行端口支持的模式。

-   **NegotiateIeeeMode**成员是指向[ **PNEGOTIATE\_IEEE\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pnegotiate_ieee_mode)回调，它设置的最快的 IEEE 通信从由调用方指定的模式中进行并行端口总线驱动程序支持的模式。

-   **TerminateIeeeMode**成员是指向[ **PTERMINATE\_IEEE\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pterminate_ieee_mode)回调，它将通信模式设置为 IEEE1284 兼容性模式。

-   **IeeeFwdToRev**成员是指向[ **PPARALLEL\_IEEE\_FWD\_TO\_REV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_ieee_fwd_to_rev)回调，这将更改从转发进行反向 （从读取的写入） 数据传输方向。

-   **IeeeRevToFwd**成员是指向[ **PPARALLEL\_IEEE\_REV\_TO\_FWD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_ieee_rev_to_fwd)回调，从反向 （从编写的读取） 转发更改的传输方向。

有关并行端口总线驱动程序支持的通信模式的详细信息，请参阅模式通过 ECP NONE\_标头文件中定义的任何*ntddpar.h* Windows Driver Kit (WDK) 中。

 

 




