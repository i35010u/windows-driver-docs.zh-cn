---
title: 微型驱动程序控制流
description: 微型驱动程序控制流
ms.assetid: c3c23d32-4023-445b-bd89-e0b454bec1ed
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，控制流
- 流式处理微型驱动程序 WDK Windows 2000 内核，控制流
- 微型驱动程序 WDK Windows 2000 内核流式处理，控制流
- 未初始化的流式处理微型驱动程序 WDK 流式处理微型驱动程序
- 初始化流式处理微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24bb312c11716a9a4921190e919c4529c294575
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348401"
---
# <a name="minidriver-flow-of-control"></a>微型驱动程序控制流





以下步骤集通常遵循在初始化、 使用和取消流微型驱动程序。 以下引用的命令和结构此文档中其他地方介绍。

**在初始化时，遵循的步骤使用，并且取消流式处理的微型驱动程序**

1.  插枚举器中检测到微型驱动程序支持的硬件适配器。 枚举器检查注册表以解析符号的任何引用，并将请求传递到 I/O 子系统。

2.  I/O 子系统加载微型驱动程序，并调用微型驱动程序的**DriverEntry**例程 (请参阅[ **Stream 类微型驱动程序的 DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff558717)) 其中[**HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)分配并初始化结构。 中的信息创建一个文件对象**DriverEntry**例程。

3.  微型驱动程序的**DriverEntry**例程然后调用流类驱动程序[ **StreamClassRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff568263)函数并传递[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构作为参数。 HW\_初始化\_数据结构包括处理 Srb 的微型驱动程序函数的地址。 这允许微型驱动程序以响应 Srb 发送的类驱动程序。

4.  在初始化期间，stream 类驱动程序调用中指定的函数[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构的**HwReceivePacket**成员 (请参阅[ *StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)) 使用和与 SRB**命令**成员设置为 SRB\_初始化\_设备。 然后，微型驱动程序初始化硬件适配器。

5.  Stream 类驱动程序调用中指定的函数[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构的**HwReceivePacket**成员使用 SRB\_获取\_流\_信息。 然后，微型驱动程序返回有关它支持的流的信息。

6.  Stream 类驱动程序调用中指定的函数**HW\_初始化\_数据**结构的**HwReceivePacket** SRB 成员\_打开\_流，与[ **HW\_流\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff559697)结构。 微型驱动程序执行必要的硬件操作，以打开指定的流。

7.  Stream 类驱动程序发送或从流请求数据，通过传递 SRB\_读取\_数据或 SRB\_编写\_数据命令中指定的函数**ReceiveDataPacket**成员的 HW\_流\_流的对象结构。

8.  Stream 类驱动程序获取和设置的属性和其他控制信息流通过传递适当的流请求块 ([**HW\_流\_请求\_块** ](https://msdn.microsoft.com/library/windows/hardware/ff559702)) 中指定的函数到**ReceiveControlPacket** HW 成员\_流\_流的对象结构。

9.  如果系统是通过使用一个流，流类驱动程序调用中指定的函数[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构的**HwReceivePacket**成员 SRB\_关闭\_流。 微型驱动程序然后关闭指定的流。

10. Stream 类驱动程序时就可以取消初始化适配器时，调用中指定的函数[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构的**HwReceivePacket**成员 SRB\_UNINITIALIZE\_设备。 微型驱动程序然后取消初始化设备。

 

 




