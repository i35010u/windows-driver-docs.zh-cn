---
title: 实现 HwVidSynchronizeExecutionCallback 例程
description: 何时实现 HwVidSynchronizeExecutionCallback 例程
ms.assetid: d33736ca-aff2-421b-a8cc-d09eba76ff7f
keywords:
- 微型端口驱动程序 WDK Windows 2000，中断
- 中断 WDK 微型端口
- HwVidSynchronizeExecutionCallback
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: fcb37f8f749cad52f39ebf59445f4348bf91685e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523001"
---
# <a name="implementing-a-hwvidsynchronizeexecutioncallback-routine"></a>实现 HwVidSynchronizeExecutionCallback 例程

适用于不很少生成中断的适配器的微型端口驱动程序调用[ **VideoPortSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff570372)与[ *HwVidSynchronizeExecutionCallback*](https://msdn.microsoft.com/library/windows/hardware/ff567369)函数。

实际上，即使有的微型端口驱动程序[ *HwVidInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff567349)函数不一定具有*HwVidSynchronizeExecutionCallback*函数。 由于视频端口驱动程序不向微型端口驱动程序发送请求[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)函数完成的上一个请求的处理之前 (请参阅[处理视频（Windows 2000 模式） 的请求](processing-video-requests--windows-2000-model-.md)有关详细信息)，微型端口驱动程序很少会调用**VideoPortSynchronizeExecution**。

有的微型端口驱动程序的两种可能用法*HwVidSynchronizeExecutionCallback*函数：

-   若要访问适配器注册为驱动程序函数使用微型端口驱动程序的设备扩展不*HwVidInterrupt*函数。

    时*HwVidSynchronizeExecutionCallback*函数提供控制，掩盖来自适配器的中断的关闭操作微型端口驱动程序*HwVidInterrupt*函数不能更改中的状态设备扩展时*HwVidSynchronizeExecutionCallback* SMP 计算机中运行函数。

-   若要编写命令对适配器寄存器或端口非常快速地适配器需要它。

    当*HwVidSynchronizeExecutionCallback*函数提供控制，几乎所有系统中断都屏蔽关闭，因此*HwVidSynchronizeExecutionCallback*函数不能被占用设备 （或甚至，一个时钟） 中断。

    *HwVidSynchronizeExecutionCallback*函数*必须*尽可能快地返回控制。

第一个类型为[ *HwVidSynchronizeExecutionCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff567369)函数、 微型端口驱动程序调用[ **VideoPortSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff570372)与*优先级*设置为**VpMediumPriority**。 第二个类型为*HwVidSynchronizeExecutionCallback*函数，微型端口驱动程序还可以使用此调用*优先级*设置为**VpMediumPriority**如果驱动程序不包含[ *HwVidInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff567349)函数。 否则，这样的微型端口驱动程序可以使用此调用*优先级*设置为**VpHighPriority**。

一般情况下，微型端口驱动程序应*不*调用**VideoPortSynchronizeExecution**第二个类型为*HwVidSynchronizeExecutionCallback*作用，除非驱动程序设计器有没有其他备用方法： 即，除非该适配器是，它必须与编程系统中断应用掩码。 否则，微型端口驱动程序应调用**VideoPortSynchronizeExecution**与*优先级*设置为**VpLowPriority**。

一个*HwVidSynchronizeExecutionCallback*函数一样， *HwVidInterrupt*函数中，不能为可分页并不能调用某些 **视频端口 * * * Xxx*函数而不会降低关闭系统。 有关的摘要 **视频端口 * * * Xxx*函数*HwVidSynchronizeExecutionCallback*函数可以安全地调用，请参阅[ *HwVidInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff567349).

 

 





