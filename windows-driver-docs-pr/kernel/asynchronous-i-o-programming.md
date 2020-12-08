---
title: 异步 I/O 编程
description: 异步 I/O 编程
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 954c2445bea6991b2087108464cfecb199fa9e1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789809"
---
# <a name="asynchronous-io-programming"></a>异步 I/O 编程


异步编程不会强制任何其他人等待。 这是编程 Windows 设备驱动程序的首选方法。 支持异步 i/o 是 WDM 驱动程序的设计目标之一。 有关驱动程序中的异步 i/o 的详细信息，请参阅 [支持异步 i/o](supporting-asynchronous-i-o.md)。 对于设备驱动程序，使用中断是异步编程的最佳方式。 只需将请求发送到设备，系统就会进行控制。 当设备想要告诉你一些内容时，它会通过调用你的驱动程序中的中断处理程序来触发操作系统处理的中断。 此通信通过 Irp 处理。 有关 IRP 的详细信息，请参阅 [处理 irp](handling-irps.md)。

 

 




