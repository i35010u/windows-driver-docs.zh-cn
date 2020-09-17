---
title: '图形体系结构中的视频微型端口驱动程序 (XDDM) '
description: 'Windows 2000 模型 (图形体系结构中的视频微型端口驱动程序) '
ms.assetid: 663cbedb-6637-4d7c-86d0-70d962459856
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，图形
- 体系结构 WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 14afbc56bf362a5b0b5536d3b6752927b599881e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715120"
---
# <a name="video-miniport-driver-in-the-graphics-architecture-windows-2000-model"></a>Windows 2000 模型 (图形体系结构中的视频微型端口驱动程序) 

下图显示了基于 NT 的操作系统图形子系统中的视频微型端口驱动程序。

![说明基于 nt 的操作系统图形体系结构的示意图](images/2vidarch.png)

每个视频微型端口驱动程序为显示驱动程序提供硬件级支持。 显示驱动程序调用 graphics engine [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 函数以从基础视频微型端口驱动程序请求支持。 接下来， **EngDeviceIoControl**调用 i/o 系统服务，通过视频端口驱动程序将请求发送到微型端口驱动程序。

在大多数情况下，显示驱动程序将执行对用户可见的时间关键操作，而基础微型端口驱动程序为不常请求的操作提供支持，或为无法被中断或上下文交换机抢占到其他进程的实际时间关键操作提供支持。

显示驱动程序无法处理设备中断，只有微型端口驱动程序可以设置设备内存，并将其映射到显示驱动程序的虚拟地址空间。

视频端口驱动程序是为支持视频微型端口驱动程序提供的系统提供的模块。 它充当显示器驱动程序和视频微型端口驱动程序之间的中介

有关基于 NT 的操作系统显示驱动程序的详细信息，请参阅 windows [2000 模型 (显示的介绍) ](introduction-to-display--windows-2000-model-.md) 和 [ (Windows 2000 模型) 显示驱动程序 ](display-drivers--windows-2000-model-.md)。

 

