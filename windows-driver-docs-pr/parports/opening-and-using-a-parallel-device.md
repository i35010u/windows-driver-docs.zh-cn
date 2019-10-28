---
title: 打开和使用并行设备
description: 打开和使用并行设备
ms.assetid: ca58b1c3-9ecf-4ebe-8f08-a2f78ae17921
keywords:
- 并行设备 WDK，打开
- 并行设备 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f64f3963361036781a4f74c42d4ff54762951a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844491"
---
# <a name="opening-and-using-a-parallel-device"></a>打开和使用并行设备





系统提供的并行端口总线驱动程序强制对连接到并行端口的并行设备进行独占访问。 如果并行设备已打开，则在关闭设备之前，并行端口总线驱动程序将无法执行任何后续[**IRP\_MJ\_** ](https://docs.microsoft.com/previous-versions/ff544131(v=vs.85))为设备创建请求。 客户端必须在将其他 i/o 请求发送到设备之前打开并行设备，或调用[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 客户端在设备上关闭其文件后，不能尝试与并行设备通信。 客户端必须关闭设备以允许其他客户端访问设备。

客户端通常会执行以下操作：

-   打开并行设备

-   连接到并行设备-请参阅[连接到并行设备](connecting-to-a-parallel-device.md)

-   获取有关并行设备的信息−参阅[获取有关并行设备的信息](obtaining-information-about-a-parallel-device.md)

-   锁定设备−参阅[锁定和解锁并行端口以供并行设备使用](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   在设备上执行一系列操作

-   与并行设备断开连接−参阅[连接到并行设备](connecting-to-a-parallel-device.md)

-   解锁设备−参阅[锁定和解锁并行端口以供并行设备使用](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   关闭设备

请注意，在即插即用环境中，每当设备上没有打开的文件时，可以删除或添加设备。 通常，每次添加并行设备时，即插即用会分配不同的位置和资源。

 

 




