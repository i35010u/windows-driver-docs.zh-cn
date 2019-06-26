---
title: 流微型驱动程序
description: 流微型驱动程序
ms.assetid: 9f669a1a-50fd-482f-a5af-28e5685dc68c
keywords:
- Windows 2000 内核流式处理模型 WDK，流式处理微型驱动程序
- 流式处理模型 WDK Windows 2000 内核，流式处理微型驱动程序
- 内核流式处理模型 WDK，流式处理微型驱动程序
- Stream.sys 类驱动程序 WDK Windows 2000 内核
- 流式处理微型驱动程序 WDK Windows 2000 内核
- 微型驱动程序 WDK Windows 2000 内核流式处理
- Stream.sys 类驱动程序 WDK Windows 2000 内核，
- 流式处理微型驱动程序 WDK Windows 2000 内核，
- 微型驱动程序 WDK Windows 2000 内核流式处理，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9250487bec1d1aa79d28c02a401a56e585d0cee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377788"
---
# <a name="streaming-minidrivers"></a>流微型驱动程序





**请注意**  本部分详细介绍过时*Stream.sys*类驱动程序。 随着 Microsoft Windows XP 的发布，Microsoft 支持*Stream.sys*仅为现有的驱动程序。 截至此版本中，Microsoft 建议，请考虑供应商开发新视频或音频/视频多媒体的驱动程序使用 AVStream 类驱动程序模型。 请参阅中的详细信息[AVStream 概述](avstream-overview.md)。 如果开发的仅限音频的驱动程序，您应编写下 Microsoft 提供的音频的微型端口驱动程序*Portcls.sys*类驱动程序。 有关详细信息，请参阅[音频微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-miniport-drivers)。

 

供应商可以通过提供在 Microsoft 提供该运行的微型驱动程序支持仅视频或音频/视频设备*Stream.sys*类驱动程序。 在此文档中，供应商提供的微型驱动程序下*Stream.sys*嘿*流式处理微型驱动程序*。

例如，可以通过流式处理微型驱动程序支持视频捕获设备和 DVD 播放机。 特定于技术的信息，请参阅[视频捕获设备](video-capture-devices.md)并[DVD 解码器微型驱动程序](dvd-decoder-minidrivers2.md)。

流式处理的微型驱动程序支持流式处理语义的内核。 若要使用本文档，驱动程序开发人员应熟悉流概念，基本内核中所述[内核流式处理](kernel-streaming.md)。

Stream 类驱动程序旨在使编写的处理很多方面与操作系统交互的流式处理更简单的设备的硬件驱动程序。

-   微型驱动程序可以允许流类驱动程序来处理代表其自身的同步。 例如，stream 类驱动程序可以根据需要序列化输入/输出请求的微型驱动程序。 允许类驱动程序来处理同步使微型驱动程序包含多个处理器安全，但 nonreentrant 处理。 这是适用于低端到中等低端硬件。

-   在类驱动程序会自动同步文件操作。 例如，在打开的流和设备进行正确序列化没有微型驱动程序使用 mutex、 信号量或事件的情况下。

-   在类驱动程序提取流语义从微型驱动程序的内核的实现。

-   在类驱动程序处理与 PnP 管理器的所有交互。 例如：
    -   在类驱动程序微型驱动程序的名义创建功能的设备对象。
    -   在类驱动程序管理资源配置 （如将端口地址转换、 转换和映射内存范围和连接中断）。
    -   在类驱动程序处理 PnP Irp，如[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)，或[ **IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)。
-   由类驱动程序处理所有低级别的缓冲区管理：
    -   如有必要，请分配 DMA 适配器对象。
    -   映射缓冲区和构建散播-聚集列出了 DMA。
    -   锁定和 DMA 和 PIO 正确刷新缓冲区。
-   所有 IOCTL 参数验证由类驱动程序都执行。

-   所有请求都使用监视程序计时器类驱动程序已都超时。

-   微型驱动程序不会创建一个设备对象，但它们共享根据需要在类驱动程序的设备对象。 这可节省系统资源。

-   每个适配器创建只有一个设备对象。 多个子设备 (称为*流*) 适配器支持的内核流式处理插针表示。

 

 




