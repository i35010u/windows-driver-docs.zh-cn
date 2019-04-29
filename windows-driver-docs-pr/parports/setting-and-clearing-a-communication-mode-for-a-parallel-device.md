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
ms.openlocfilehash: 4a2680d79b405c41a4c6c9f03f42ebb6319e58ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380550"
---
# <a name="setting-and-clearing-a-communication-mode-for-a-parallel-device"></a>设置和清除并行设备的通信模式





客户端可以设置使用以下设备控制请求的并行设备的通信模式：

-   [**IOCTL\_IEEE1284\_获取\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff543975)返回当前在设备上设置的通信协议。 端口没有要锁定用于此请求。

-   [**IOCTL\_IEEE1284\_NEGOTIATE** ](https://msdn.microsoft.com/library/windows/hardware/ff543978)协商新的通信模式。 必须分配的并行端口并选择 IEEE 1284.3 设备。

-   [**IOCTL\_内部\_断开连接\_空闲**](https://msdn.microsoft.com/library/windows/hardware/ff543993)通信模式设置为 IEEE\_兼容。 必须分配的并行端口并选择 IEEE 1284.3 设备。

内核模式驱动程序还可以使用系统提供[并行设备回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544275)。 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff544040)请求将返回[ **PARCLASS\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544334)结构，其中包含以下系统提供的回调例程的指针：

-   **DetermineIeeeMode**成员是指向[ **PDETERMINE\_IEEE\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff544365)回调，它确定 IEEE 通信并行端口支持的模式。

-   **NegotiateIeeeMode**成员是指向[ **PNEGOTIATE\_IEEE\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff544386)回调，它设置的最快的 IEEE 通信从由调用方指定的模式中进行并行端口总线驱动程序支持的模式。

-   **TerminateIeeeMode**成员是指向[ **PTERMINATE\_IEEE\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff544773)回调，它将通信模式设置为 IEEE1284 兼容性模式。

-   **IeeeFwdToRev**成员是指向[ **PPARALLEL\_IEEE\_FWD\_TO\_REV** ](https://msdn.microsoft.com/library/windows/hardware/ff544524)回调，这将更改从转发进行反向 （从读取的写入） 数据传输方向。

-   **IeeeRevToFwd**成员是指向[ **PPARALLEL\_IEEE\_REV\_TO\_FWD** ](https://msdn.microsoft.com/library/windows/hardware/ff544528)回调，从反向 （从编写的读取） 转发更改的传输方向。

有关并行端口总线驱动程序支持的通信模式的详细信息，请参阅模式通过 ECP NONE\_标头文件中定义的任何*ntddpar.h* Windows Driver Kit (WDK) 中。

 

 




