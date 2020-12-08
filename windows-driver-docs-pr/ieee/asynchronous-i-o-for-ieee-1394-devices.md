---
title: IEEE 1394 设备的异步 I/O
description: IEEE 1394 设备的异步 I/O
keywords:
- IEEE 1394 WDK 总线，异步 i/o
- 1394 WDK 总线，异步 i/o
- 异步 i/o WDK IEEE 1394 总线
- I/o WDK IEEE 1394 总线
- I/o 请求数据包 WDK IEEE 1394 总线
- Irp WDK IEEE 1394 总线
- 传输数据 WDK IEEE 1394 总线
- PDOs WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b31d685fecd905a5b1023a9d5c0020ad4cc480
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794959"
---
# <a name="asynchronous-io-for-ieee-1394-devices"></a>IEEE 1394 设备的异步 I/O





IEEE 1394 总线上的设备在异步模式下通过发送和接收数据包进行通信。 设备将读取、写入和锁定请求发送到另一个设备的地址空间中的特定地址。 为提供服务质量，接收设备完成请求时，会将响应数据包发送回发送设备，然后发送响应确认。

驱动程序可以通过向设备发送异步 i/o 请求来与设备进行通信。 驱动程序还可以分配主机计算机的 IEEE 1394 地址空间中的地址范围，并接收对这些地址的请求。 以下各部分介绍了这两种方法：

[在 IEEE 1394 总线上发送异步 I/O 请求数据包](./sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus.md)

[在 IEEE 1394 总线上接收异步 I/O 请求数据包](./receiving-asynchronous-i-o-request-packets-on-the-ieee-1394-bus.md)

 

