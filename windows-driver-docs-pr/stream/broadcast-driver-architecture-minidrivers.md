---
title: 广播驱动程序体系结构微型驱动程序
description: 广播驱动程序体系结构微型驱动程序
keywords:
- 广播驱动程序体系结构 WDK AVStream，微型驱动程序
- BDA WDK AVStream，微型驱动程序
- 微型驱动程序 WDK BDA
- BDA 微型驱动程序 WDK AVStream
- BDA 微型驱动程序 WDK AVStream，关于 BDA 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7b82d133e312f3ae692607586c8cf06dfed7d40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833985"
---
# <a name="broadcast-driver-architecture-minidrivers"></a>广播驱动程序体系结构微型驱动程序





广播驱动程序体系结构 (BDA) 微型驱动程序控制硬件执行以下操作：

-   调整数字广播信号

-   Demodulating 数字信号

-   捕获数字信号的帧

-   将信号 Demultiplexing 视频、音频和数据流

BDA 微型驱动程序是 AVStream 微型驱动程序，它在内核流式处理驱动程序 *ks.sys* 中的 [AVStream 模块](avstream-overview.md)下运行。 AVStream 是一种类驱动程序，它为音频和视频微型驱动程序提供统一的内核流式处理类模型，并且支持使用 COM 对象，而无需更改现有的微型驱动程序二进制文件。 AVStream 类驱动程序提供将微型驱动程序的筛选器作为 WDM 内核流式处理兼容筛选器工作所需的大部分默认行为。 若要简化写入 BDA 微型驱动程序的任务，你可以使用 BDA 支持 (库) Microsoft Windows 驱动程序工具包 (WDK) 中包含的函数 *。* 此库为 BDA 微型驱动程序的属性和方法集提供了广泛的默认处理。

通常，驱动程序编写器只需编写相应的静态模板结构的代码，将其注册到 BDA 支持库，然后让库为所有属性和方法提供默认处理。 在某些情况下，BDA 微型驱动程序必须截获属性或方法请求并执行适当的操作。

下图显示了 BDA 微型驱动程序的体系结构概述：

![bda 微型驱动程序体系结构图示概述](images/bdaarch.png)

以下各节描述了 BDA 微型驱动程序的实现详细信息，讨论一些属性和方法集的详细信息，并包含演示如何截获某些属性和方法的示例代码：

[初始化 BDA 微型驱动程序](initializing-a-bda-minidriver.md)

[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)

[创建调度表](creating-dispatch-tables.md)

[定义自动化表](defining-automation-tables.md)

[初始化 BDA 筛选器](initializing-a-bda-filter.md)

[使用 BDA 属性和方法集](using-bda-property-and-method-sets.md)

[缓存 DirectShow 的引脚信息](caching-pin-information-for-directshow.md)

[保护 BDA 微型驱动程序](securing-a-bda-minidriver.md)

[在 BDA 微型驱动程序筛选器的引脚之间进行连接](connecting-between-pins-of-filters-for-bda-minidrivers.md)

 

 




