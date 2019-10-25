---
title: 设置和清除并行设备的通信模式
description: 设置和清除并行设备的通信模式
ms.assetid: 2ff53ed0-dbb7-4c8f-b6e4-5f7d20124a7c
keywords:
- 并行设备 WDK，通信模式
- 通信模式 WDK 并行设备
- 清除通信模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7abc68f65e1a9076251efdb33ed57d8dd4282ee3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842323"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>设置和清除并行设备的通信模式





客户端可以使用以下设备控制请求设置并行设备的通信模式：

-   [**IOCTL\_IEEE1284\_GET\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)返回设备上设置的当前通信协议。 不必锁定端口即可使用此请求。

-   [**IOCTL\_IEEE1284\_协商**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)协商新的通信模式。 必须分配并行端口，并选择 IEEE 1284.3 设备。

-   [**IOCTL\_内部\_断开连接\_空闲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_disconnect_idle)将通信模式设置为与 IEEE\_兼容。 必须分配并行端口，并选择 IEEE 1284.3 设备。

内核模式驱动程序还可以使用系统提供的[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 [**IOCTL\_内部\_PARCLASS\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)请求返回[**PARCLASS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)结构，其中包括指向系统提供的回调例程的以下指针：

-   **DetermineIeeeMode**成员是指向[**PDETERMINE\_ieee\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pdetermine_ieee_modes)回调的指针，它确定并行端口支持的 ieee 通信模式。

-   **NegotiateIeeeMode**成员是指向[**PNEGOTIATE\_ieee\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pnegotiate_ieee_mode)回拨的指针，它可以在调用方指定的模式之间设置并行端口总线驱动程序支持的最快 IEEE 通信模式。

-   **TerminateIeeeMode**成员是指向[**PTERMINATE\_ieee\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pterminate_ieee_mode)回调的指针，它将通信模式设置为 ieee 1284 兼容模式。

-   **IeeeFwdToRev**成员是指向[**PPARALLEL\_IEEE\_FWD\_到\_REV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_fwd_to_rev)回叫的指针，它将数据传输方向从 forward 改为反转（从写入到读取）。

-   **IeeeRevToFwd**成员是指向[**PPARALLEL\_IEEE\_REV\_\_FWD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_ieee_rev_to_fwd)回拨的指针，它将传输方向从反向改为向前（从读取到写入）。

有关并行端口总线驱动程序支持的通信模式的详细信息，请参阅 NONE 到 ECP 的模式\_在 Windows 驱动程序工具包（WDK）中的头文件*ntddpar*中定义的任何模式。

 

 




