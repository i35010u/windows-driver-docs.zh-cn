---
title: 内核流式处理
description: 内核流式处理
ms.assetid: dcd28218-b3bf-4e5d-b1a7-6910103afb96
keywords:
- Windows 2000 内核流式处理模型 WDK，内核流式处理
- 流式处理模型 WDK Windows 2000 内核，内核流式处理
- 内核流式处理模型 WDK，内核流式处理
- 内核流式处理 WDK
- 内核流 WDK，关于内核流式处理
- KS WDK
- KS WDK，关于内核流式处理
- 微型驱动程序 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c95b5a984dad9fd88835f0f68cf324f658554d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845560"
---
# <a name="kernel-streaming"></a>内核流式处理





内核流式处理（KS）是指 Microsoft 提供的服务，支持对流式数据进行内核模式处理。

Microsoft 提供了三种多媒体类驱动程序模型： port class、stream 类和 AVStream。 供应商编写在这三个类驱动程序模型之一下运行的微型驱动程序。

这些类驱动程序在系统文件*portcls* *、http.sys 和* *ks*中实现为导出驱动程序（内核模式 dll）。 在 Windows XP 和更高版本中， *sys.databases*称为 AVStream。

在 Windows XP SP2 和更高版本中，Microsoft 提供了[USB 视频类](usb-video-class-driver.md)驱动程序。

本部分包含有关以下主题的旧版文档，这些主题与原始（XP XP XP） *ks*类驱动程序相关：

[KS 微型驱动程序体系结构](ks-minidriver-architecture.md)

[KS 属性、事件和方法](ks-properties--events--and-methods.md)

[KS 时钟](ks-clocks.md)

[KS 分配器](ks-allocators.md)

有关*portcls*的详细信息，请参阅[音频驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/index)。

若要了解有关*http.sys*驱动程序的信息，请参阅[流式处理微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)。

若要阅读有关 AVStream 的信息，请参阅[AVStream 概述](avstream-overview.md)。

[DVD 解码器微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)是*http.sys*的客户端。

[视频捕获微型驱动程序](video-capture-devices.md)*可以是*或*ks*的客户端。

[广播驱动程序体系结构微型驱动程序](broadcast-driver-architecture-minidrivers.md)在 AVStream 下运行。

 

 




