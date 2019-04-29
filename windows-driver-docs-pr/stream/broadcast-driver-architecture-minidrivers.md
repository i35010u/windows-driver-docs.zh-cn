---
title: 广播驱动程序体系结构微型驱动程序
description: 广播驱动程序体系结构微型驱动程序
ms.assetid: 0ad56dbd-6f79-439f-8dfc-8d118d114ddd
keywords:
- 广播驱动程序体系结构 WDK AVStream，微型驱动程序
- BDA WDK AVStream，微型驱动程序
- 微型驱动程序 WDK BDA
- BDA 微型驱动程序 WDK AVStream
- BDA 微型驱动程序 WDK AVStream 有关 BDA 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66199c036d4c62916810700d4a0e93e3faf43b59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370433"
---
# <a name="broadcast-driver-architecture-minidrivers"></a>广播驱动程序体系结构微型驱动程序





广播驱动程序体系结构 (BDA) 微型驱动程序控制硬件，执行以下操作：

-   优化数字广播的信号

-   解调数字信号

-   捕获帧的数字信号

-   为视频、 音频和数据的流将信号解多路复用

BDA 微型驱动程序是 AVStream 下运行的微型驱动程序[AVStream 模块](avstream-overview.md)内核流式处理驱动程序中*ks.sys*。 AVStream 是类驱动程序，它提供一个统一的内核类将模型流式传输音频和视频微型驱动程序，为和的支持使用 COM 对象，而无需更改现有的微型驱动程序二进制文件。 AVStream 类驱动程序提供了许多作为 WDM 核心流式处理兼容的筛选器使微型驱动程序的筛选器工作所需的默认行为。 若要简化编写 BDA 微型驱动程序的任务，可以使用 BDA 支持库 (*Bdasup.lib*) 的 Microsoft Windows Driver Kit (WDK) 中包含的函数。 此库提供广泛的默认处理 BDA 微型驱动程序的属性和方法集。

通常情况下，驱动程序编写人员只需编码的相应静态模板结构、 注册 BDA 支持库，然后让库提供默认处理的所有属性和方法。 在某些情况下，BDA 微型驱动程序必须截获属性或方法的请求并执行相应操作。

下图显示了 BDA 微型驱动程序的体系结构概述：

![bda 微型驱动程序体系结构关系图概述](images/bdaarch.png)

以下各节介绍的 BDA 微型驱动程序实现的详细信息、 讨论的某些属性和方法集，详细信息和包含的代码示例演示如何以截获某些属性和方法：

[初始化 BDA 微型驱动程序](initializing-a-bda-minidriver.md)

[启动 BDA 微型驱动程序](starting-a-bda-minidriver.md)

[创建调度表](creating-dispatch-tables.md)

[定义自动化表](defining-automation-tables.md)

[初始化 BDA 筛选器](initializing-a-bda-filter.md)

[使用 BDA 属性和方法集](using-bda-property-and-method-sets.md)

[Directshow 缓存 Pin 信息](caching-pin-information-for-directshow.md)

[保护 BDA 微型驱动程序](securing-a-bda-minidriver.md)

[Pin BDA 微型驱动程序的筛选器之间的连接](connecting-between-pins-of-filters-for-bda-minidrivers.md)

 

 




