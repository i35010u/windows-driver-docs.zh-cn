---
title: 在图形体系结构 (XDDM) 中的视频微型端口驱动程序
description: 在图形体系结构 （Windows 2000 模式） 中的视频微型端口驱动程序
ms.assetid: 663cbedb-6637-4d7c-86d0-70d962459856
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，图形
- 体系结构 WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: cf723c032c5e39918ecf503c9eb3aeb8582d0fef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554528"
---
# <a name="video-miniport-driver-in-the-graphics-architecture-windows-2000-model"></a>在图形体系结构 （Windows 2000 模式） 中的视频微型端口驱动程序

下图显示了基于 NT 的操作系统图形子系统中的微型端口驱动程序。

![说明在基于 nt 的操作系统图形体系结构的关系图](images/2vidarch.png)

每个视频的微型端口驱动程序的显示驱动程序提供硬件级别的支持。 显示驱动程序调用图形引擎[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)函数来从基础的微型端口驱动程序请求支持。 **EngDeviceIoControl**，反过来，调用 I/O 系统服务将通过视频端口驱动程序将请求发送到微型端口驱动程序。

在大多数情况下，显示器驱动程序执行是对用户可见的而基础的微型端口驱动程序提供支持，用于不常请求的操作或不能为的真正时间关键操作的时间关键操作通过中断或上下文切换到另一个进程已占用。

显示驱动程序不能处理设备中断，并仅微型端口驱动程序可以设置设备内存并将其映射到显示器驱动程序的虚拟地址空间。

视频端口驱动程序是系统提供的模块提供用于支持视频的微型端口驱动程序。 它充当显示器驱动程序和视频的微型端口驱动程序之间的媒介

有关在基于 NT 的操作系统显示驱动程序的详细信息，请参阅[简介 （Windows 2000 模式） 显示](introduction-to-display--windows-2000-model-.md)并[显示驱动程序 （Windows 2000 模式）](display-drivers--windows-2000-model-.md)。

 

 





