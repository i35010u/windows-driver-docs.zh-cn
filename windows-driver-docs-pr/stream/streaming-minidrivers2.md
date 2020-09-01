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
- 流式传输微型驱动程序 WDK Windows 2000 内核，
- 微型驱动程序 WDK Windows 2000 内核流式处理，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05561488d3d0e499ade784ba939beef544c15649
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190347"
---
# <a name="streaming-minidrivers"></a>流微型驱动程序





**注意**   本部分详细介绍过时的*Stream.sys*类驱动程序。 随着 Microsoft Windows XP 的发布，Microsoft 仅支持现有驱动程序的 *Stream.sys* 。 在此版本中，Microsoft 建议供应商考虑使用 AVStream 类驱动程序模型开发新的视频或音频/视频多媒体驱动程序。 请参阅 [AVStream 概述](avstream-overview.md)中的详细信息。 如果要开发仅音频驱动程序，则应在 Microsoft 提供的 *Portcls.sys* 类驱动程序下编写音频微型端口驱动程序。 有关详细信息，请参阅 [音频微型端口驱动程序](../audio/audio-miniport-drivers.md)。

 

供应商可以通过提供一个在 Microsoft 提供的 *Stream.sys* 类驱动程序下运行的微型驱动程序，来支持仅视频或音频/视频设备。 在本文档中，在 *Stream.sys* 下，供应商提供的微型驱动程序称为 *流式处理微型驱动程序*。

例如，流式传输微型驱动程序可支持视频捕获设备和 DVD 播放机。 有关特定于技术的信息，请参阅 [视频捕获设备](video-capture-devices.md) 和 [DVD 解码器微型驱动程序](dvd-decoder-minidrivers2.md)。

流式处理微型驱动程序支持内核流语义。 若要使用本文档，驱动程序开发人员应熟悉基本内核流式处理概念，如 [内核流](kernel-streaming.md)中所述。

流类驱动程序旨在通过处理与操作系统交互的许多方面，使写入流式处理设备的硬件驱动程序更简单。

-   微型驱动程序可以允许 stream 类驱动程序代表其处理同步。 例如，stream 类驱动程序可以有选择地序列化微型驱动程序的 i/o 请求。 允许类驱动程序处理同步会使微型驱动程序多处理器安全，但 nonreentrant。 这适用于低端到中端硬件。

-   类驱动程序会自动同步文件操作。 例如，如果没有使用互斥体、信号或事件的微型驱动程序，则会正确序列化流和设备的打开。

-   类驱动程序从微型驱动程序抽象内核流语义的实现。

-   类驱动程序处理与 PnP 管理器的所有交互。 例如：
    -   类驱动程序代表微型驱动程序创建功能设备对象。
    -   类驱动程序管理资源配置 (例如，转换端口地址、转换和映射内存范围以及连接中断) 。
    -   类驱动程序处理 PnP Irp，如 [**irp \_ MN \_ START \_ device**](../kernel/irp-mn-start-device.md)或 [**irp \_ MN \_ STOP \_ device**](../kernel/irp-mn-stop-device.md)。
-   类驱动程序处理所有低级别缓冲区管理：
    -   如有必要，分配 DMA 适配器对象。
    -   为 DMA 映射缓冲区并构建分散/收集列表。
    -   为 DMA 和 PIO 正确锁定并刷新缓冲区。
-   所有 IOCTL 参数验证由类驱动程序执行。

-   类驱动程序使用监视程序计时器对所有请求进行计时。

-   微型驱动程序不会创建设备对象，但会根据需要共享类驱动程序的设备对象。 这将保存系统资源。

-   每个适配器只创建一个设备对象。 适配器支持的多个 subdevices (称为 *流*) 由内核流 pin 表示。

 

