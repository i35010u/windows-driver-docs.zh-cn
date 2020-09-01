---
title: 在视频微型端口驱动程序中注册回调函数
description: 视频微型端口驱动程序中单独注册的回调函数
ms.assetid: 18469b9b-aca4-4225-97d0-8cafe64b8e1f
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，回调函数
- 回调函数 WDK 视频微型端口
- 单独注册的回调函数 WDK 视频微型端口
- 注册的回调函数 WDK 视频微型端口
- 临时注册 WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 32cf25eb69e05d519be73ebfee9389531f84b046
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064768"
---
# <a name="registering-callback-functions-in-video-miniport-drivers"></a>在视频微型端口驱动程序中注册回调函数

在某些情况下，供应商提供的视频微型端口驱动程序与系统提供的视频端口驱动程序之间的通信将按如下方式进行：

1.  视频微型端口驱动程序调用视频端口驱动程序中的函数。

2.  视频端口驱动程序功能完成前，它会回拨到视频微型端口驱动程序以获得帮助。

当视频微型端口驱动程序调用视频端口驱动程序函数时，它会传递一个指向回调函数的指针。 例如，当视频微型端口驱动程序调用 [**VideoPortStartDma**](/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)时，它会将指向 *HwVidExecuteDma* 回调函数的指针传递 (由视频微型端口驱动程序) 实现。

当视频微型端口驱动程序将回调函数的地址传递给视频端口驱动程序函数时，它会向视频端口驱动程序 *注册* 回调函数。 注册是临时性的，因为视频端口驱动程序不会永久存储回调函数指针。 相反，视频端口驱动程序只会在执行回调的函数期间保存函数指针。 这种类型的临时注册与许多视频微型端口驱动程序函数的永久注册相反。 例如，视频微型端口驱动程序在 **DriverEntry**期间注册一组函数，视频端口驱动程序会将这些函数指针永久地存储在设备扩展中。

在某些情况下，视频微型端口驱动程序实现多个功能是有意义的，其中每个函数都可以充当特定视频端口驱动程序函数的回调函数。 例如，视频微型端口驱动程序可能会实现 *HwVidQueryDeviceCallback* 函数的多个变体，并在对 [**VideoPortGetDeviceData**](/windows-hardware/drivers/ddi/video/nf-video-videoportgetdevicedata)的特定调用中传递选择的变体。

有关可由视频微型端口驱动程序实现的回调函数的列表，以及有关如何注册这些回调函数的信息，请参阅 [单独注册的视频微型端口驱动程序函数](/windows-hardware/drivers/ddi/index)。