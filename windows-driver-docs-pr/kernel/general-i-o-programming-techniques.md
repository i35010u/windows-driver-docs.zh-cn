---
title: 常规 I/O 编程技术
description: 常规 I/O 编程技术
ms.assetid: c310829f-e102-4a96-aa3e-39136b8a641b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0da47330b740ee894dc5dcd0ed09fca742af599
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403456"
---
# <a name="general-io-programming-techniques"></a>常规 I/O 编程技术


I/o 编程中最重要的一种方法是应避免的操作：强制操作系统等待你的设备。 几乎每个人都有权看到 Microsoft Windows "冻结"。 有时冻结是由于崩溃造成的，而另一些时候系统只是等待设备响应。

有两种基本编程技术可用于处理等待设备： *同步* 和 *异步*操作。 同步编程等待设备，应避免这样做。 异步编程使用其他技术 (例如等待中断请求) 。 有关同步和异步编程的详细信息，请参阅以下主题：

[同步 I/O 编程](synchronous-i-o-programming.md)

[异步 I/O 编程](asynchronous-i-o-programming.md)

Microsoft Vista 提供了一个新的策略，用于处理同步编程的问题。 有关此新策略的详细信息，请参阅 [在 Windows Vista 中限制等待](restricting-waits-in-vista.md) 以获取详细信息。

在早期的设备驱动程序编程中，驱动程序需要重复从驱动程序请求信息，直到提供答案。 此方法称为轮询，几乎不能使用。 处理轮询问题的最佳方式是使用硬件中断。 有关硬件中断的详细信息，请参阅 [服务中断](introduction-to-interrupt-service-routines.md)。 有关轮询的详细信息以及不应使用它的原因，请参阅 [避免设备轮询](avoid-polling-devices.md)。

 

 




