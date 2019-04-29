---
title: 内核流式处理
description: 内核流式处理
ms.assetid: dcd28218-b3bf-4e5d-b1a7-6910103afb96
keywords:
- Windows 2000 内核流式处理模型 WDK，流式处理的内核
- 流式处理模型 WDK Windows 2000 内核，流式处理的内核
- 内核流式处理模型 WDK，流式处理的内核
- 流式处理 WDK 的内核
- 有关内核流式处理流 WDK，内核
- KS WDK
- KS WDK，有关内核流式处理
- 流式处理的微型驱动程序 WDK 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69095716a217e18fb93825f1c2fff581d2865cd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376475"
---
# <a name="kernel-streaming"></a>内核流式处理





内核流式处理 (KS) 是经过流处理数据的支持内核模式下处理指由 Microsoft 提供服务。

Microsoft 提供了三个多媒体类驱动程序模型： 类、 流类和 AVStream 的端口。 供应商将写入一个这些三个类驱动程序模型下运行的微型驱动程序。

这些类驱动程序被实现为导出的系统文件中的驱动程序 (内核模式 Dll) *portcls.sys*， *stream.sys*，并*ks.sys*。 在 Windows XP 及更高版本， *ks.sys*称为 AVStream。

在 Windows XP SP2 和更高版本，Microsoft 提供了[USB 视频类](usb-video-class-driver.md)驱动程序。

本部分包含与原始 (预 XP) 相关的以下主题中的旧文档*ks.sys*类驱动程序：

[KS 微型驱动程序体系结构](ks-minidriver-architecture.md)

[KS 属性、 事件和方法](ks-properties--events--and-methods.md)

[KS 时钟](ks-clocks.md)

[KS 分配器](ks-allocators.md)

有关详细信息*portcls.sys*，请参阅[音频驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff536191)。

若要了解如何*stream.sys*驱动程序，请参阅[流式处理微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff568275)。

若要阅读有关 AVStream 信息，请参阅[AVStream 概述](avstream-overview.md)。

[DVD 解码器微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff558742)的客户端*stream.sys*。

[视频捕获微型驱动程序](video-capture-devices.md)可以是任何一个客户端*stream.sys*或*ks.sys*。

[广播驱动程序体系结构微型驱动程序](broadcast-driver-architecture-minidrivers.md)AVStream 下运行。

 

 




