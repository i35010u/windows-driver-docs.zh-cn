---
title: 打开和使用并行设备
description: 打开和使用并行设备
ms.assetid: ca58b1c3-9ecf-4ebe-8f08-a2f78ae17921
keywords:
- 并行设备 WDK，打开
- 并行设备 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f3713c9975f9142e854da242305f6bc6dc276af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358506"
---
# <a name="opening-and-using-a-parallel-device"></a>打开和使用并行设备





并行端口的系统提供的总线驱动程序强制执行到并行设备附加到并行端口的独占访问。 如果并行设备处于打开状态，并行端口总线驱动程序失败，任何后续[ **IRP\_MJ\_创建**](https://docs.microsoft.com/previous-versions/ff544131(v=vs.85))设备在关闭设备之前的请求。 其他输入/输出请求发送到设备或调用之前，必须打开并行设备客户端[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 客户端必须尝试后客户端已关闭其设备上的文件与并行设备进行通信。 客户端必须先关闭设备以允许访问设备的其他客户端。

客户端通常执行以下操作：

-   打开并行设备

-   连接到并行设备 −，请参阅[连接到并行的设备](connecting-to-a-parallel-device.md)

-   获取有关并行设备 − 详细信息，参阅信息[获取并行设备信息](obtaining-information-about-a-parallel-device.md)

-   锁定设备 − 详细信息，参阅[锁定和解锁并行设备使用的并行端口](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   Does 一系列设备上的操作

-   断开并行设备 −，请参阅[连接到并行的设备](connecting-to-a-parallel-device.md)

-   解锁设备 − 详细信息，参阅[锁定和解锁并行设备使用的并行端口](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   关闭设备

请注意，在插环境中，设备可以删除或添加任何打开的文件时。 一般情况下，每次添加并行设备，插分配不同的位置和资源。

 

 




