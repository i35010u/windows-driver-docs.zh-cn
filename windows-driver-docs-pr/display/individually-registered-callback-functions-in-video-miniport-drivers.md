---
title: 在视频微型端口驱动程序中注册回调函数
description: 分别在视频微型端口驱动程序中注册回调函数
ms.assetid: 18469b9b-aca4-4225-97d0-8cafe64b8e1f
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，回调函数
- 回调函数 WDK 微型端口
- 单独注册的回调函数 WDK 微型端口
- 注册的回调函数 WDK 微型端口
- 临时注册 WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: e3c58de521eb796107d9e6fa714bb124d6008435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325053"
---
# <a name="registering-callback-functions-in-video-miniport-drivers"></a>在视频微型端口驱动程序中注册回调函数

在某些情况下，供应商提供微型端口驱动程序和系统提供的视频端口驱动程序之间的通信将继续，按如下所示：

1.  微型端口驱动程序的视频端口驱动程序中调用的函数。

2.  视频端口驱动程序函数完成之前，该回调到微型端口驱动程序以获得帮助。

当视频微型端口驱动程序调用的视频端口驱动程序函数时，它将指针传递给回调函数。 例如，当微型端口驱动程序调用[ **VideoPortStartDma**](https://msdn.microsoft.com/library/windows/hardware/ff570369)，它将传递一个指向*HwVidExecuteDma* （由视频实现的回调函数微型端口驱动程序）。

微型端口驱动程序将回调函数的地址传递给视频端口驱动程序函数时它*注册*具有视频端口驱动程序的回调函数。 临时的视频端口驱动程序不会永久存储回调函数指针在意义上注册。 相反，视频端口驱动程序仅在回调函数的执行期间保存函数指针。 这种类型的临时注册的是与很多微型端口驱动程序函数的永久注册。 例如，视频微型端口驱动程序注册过程中起作用的一组**DriverEntry**，和的视频端口驱动程序存储这些函数指针永久设备扩展中。

在某些情况下，有意义的微型端口驱动程序实现了多种功能，其中每个可用作特定视频端口驱动程序函数的回调函数。 例如，视频微型端口驱动程序可以实现的多种变体*HwVidQueryDeviceCallback*函数并传递到特定的调用中所选的变体[ **VideoPortGetDeviceData**](https://msdn.microsoft.com/library/windows/hardware/ff570311).

可以由微型端口驱动程序实现的回调函数的列表以及有关如何注册这些回调函数的信息，请参阅[单独注册视频微型端口驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff567672)。