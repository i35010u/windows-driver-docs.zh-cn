---
title: 用户模式和内核模式
description: 用户模式和内核模式
ms.assetid: 9988ff75-f84e-404e-8c2b-0f8325fbbc63
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 370f5ef3e5e1b9a5880646e551cdf5e5af37b224
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371196"
---
# <a name="user-mode-and-kernel-mode"></a>用户模式和内核模式


运行 Windows 的计算机中的处理器有两个不同模式：用户模式  和内核模式  。 根据处理器上运行的代码的类型，处理器在两个模式之间切换。 应用程序在用户模式下运行，核心操作系统组件在内核模式下运行。 虽然许多驱动程序以内核模式运行，但某些驱动程序可能以用户模式运行。

启动用户模式应用程序时，Windows 会为该应用程序创建进程  。 进程为应用程序提供专用的“虚拟地址空间”  和专用的“句柄表”  。 由于应用程序的虚拟地址空间为专用空间，因此一个应用程序无法更改属于其他应用程序的数据。 每个应用程序都隔离运行，如果一个应用程序发生故障，则故障仅局限于该应用程序。 其他应用程序和操作系统不会受该故障的影响。

除了专用之外，用户模式应用程序的虚拟地址空间也受到限制。 在用户模式下运行的处理器无法访问为操作系统保留的虚拟地址。 限制用户模式应用程序的虚拟地址空间可防止应用程序更改以及可能损坏关键的操作系统数据。

在内核模式下运行的所有代码都共享单个虚拟地址空间。 这意味着内核模式驱动程序不会与其他驱动程序和操作系统本身隔离。 如果内核模式驱动程序意外写入错误的虚拟地址，则属于操作系统或其他驱动程序的数据可能会受到安全威胁。 如果内核模式驱动程序发生故障，整个操作系统就会发生故障。

此图说明了用户模式组件与内核模式组件之间的通信。

![框图：用户模式组件和内核模式组件](images/userandkernelmode01.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[虚拟地址空间](virtual-address-spaces.md)

 

 






