---
title: 设置和清除并行设备的通信模式
description: 设置和清除并行设备的通信模式
keywords:
- 并行设备 WDK，通信模式
- 通信模式 WDK 并行设备
- 清除通信模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c9ad474b3555526342ba63c22db46ca70fbd5c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806085"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>设置和清除并行设备的通信模式





客户端可以使用以下设备控制请求设置并行设备的通信模式：

-   [**IOCTL \_IEEE1284 \_ 获取 \_ 模式**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode) 返回设备上设置的当前通信协议。 不必锁定端口即可使用此请求。

-   [**IOCTL \_IEEE1284 \_ 协商**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate) 协商新的通信模式。 必须分配并行端口，并选择 IEEE 1284.3 设备。

-   [**IOCTL \_内部 \_ 断开连接 \_ 空闲**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_disconnect_idle) 设置与 IEEE 兼容的通信模式 \_ 。 必须分配并行端口，并选择 IEEE 1284.3 设备。

内核模式驱动程序还可以使用系统提供的 [并行设备回调例程](/windows-hardware/drivers/ddi/index)。 [**IOCTL \_ 内部 \_ PARCLASS \_ 连接**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)请求将返回一个 [**PARCLASS \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)结构，其中包括指向系统提供的回调例程的以下指针：

-   **DetermineIeeeMode** 成员是指向 [**PDETERMINE \_ ieee \_ 模式**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pdetermine_ieee_modes)回调的指针，它确定并行端口支持的 ieee 通信模式。

-   **NegotiateIeeeMode** 成员是指向 [**PNEGOTIATE \_ ieee \_ 模式**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pnegotiate_ieee_mode)回调的指针，它可设置并行端口总线驱动程序在由调用方指定的模式之间支持的最快 IEEE 通信模式。

-   **TerminateIeeeMode** 成员是指向 [**PTERMINATE \_ ieee \_ 模式**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pterminate_ieee_mode)回调的指针，它将通信模式设置为 ieee 1284 兼容模式。

-   **IeeeFwdToRev** 成员是指向 [**PPARALLEL \_ IEEE \_ FWD \_ to \_ REV**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_fwd_to_rev)回拨的指针，它将数据传输方向从 "写入" 更改 (从 "写入" 改为 "读取") 。

-   **IeeeRevToFwd** 成员是指向 FWD 回调的 [**PPARALLEL \_ IEEE \_ REV \_ \_**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_rev_to_fwd)的指针，它将传输方向从 "反向" 改为 "向前" (从 "读取" 更改为 "写入") 。

有关并行端口总线驱动程序支持的通信模式的详细信息，请参阅 \_ Windows 驱动程序工具包 (WDK) 中的标头文件 *ntddpar* 中定义的所有模式。

 

