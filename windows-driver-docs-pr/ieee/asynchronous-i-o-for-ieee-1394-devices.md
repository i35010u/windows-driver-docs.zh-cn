---
title: IEEE 1394 设备的异步 I/O
description: IEEE 1394 设备的异步 I/O
ms.assetid: 36ca83d9-83ed-4366-81e7-63c5337f8643
keywords:
- IEEE 1394 WDK 总线，异步 I/O
- 1394 WDK 总线，异步 I/O
- 异步 I/O WDK IEEE 1394 总线
- I/O WDK IEEE 1394 总线
- I/O 请求数据包 WDK IEEE 1394 总线
- Irp WDK IEEE 1394 总线
- 传输数据 WDK IEEE 1394 总线
- PDOs WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f939f719e3b7bdf37ab28541b71173bb1eb955
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376713"
---
# <a name="asynchronous-io-for-ieee-1394-devices"></a>IEEE 1394 设备的异步 I/O





IEEE 1394 总线上的设备进行通信，在异步模式下，通过发送和接收数据包。 设备发送读取、 写入和锁定到另一台设备的地址空间中的特定地址的请求。 若要提供服务质量，接收设备完成请求时，它将响应数据包发送回发送设备，然后将发送一个响应确认。

驱动程序可以通过将异步 I/O 请求发送到设备通信到其设备。 驱动程序还可以分配的主计算机的 IEEE 1394 地址空间中的地址范围，并接收到指定的地址的请求。 两者都记录在以下各节中：

[IEEE 1394 总线上发送的异步 I/O 请求数据包](https://msdn.microsoft.com/library/windows/hardware/ff538087)

[IEEE 1394 总线上的异步 I/O 请求数据包的接收](https://msdn.microsoft.com/library/windows/hardware/ff537626)

 

 




