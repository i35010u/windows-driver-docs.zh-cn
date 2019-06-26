---
title: 视频捕获设备
description: 视频捕获设备
ms.assetid: ed02e6c8-fd82-488b-a0dc-8e83a842bcc4
keywords:
- 捕获视频 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc7c183941dea50a9a9609c39274142148f8ea77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385384"
---
# <a name="video-capture-devices"></a>视频捕获设备


本部分介绍如何创建视频捕获微型驱动程序，其遵循 Windows 驱动程序模型 (WDM) 体系结构。 它假定你熟悉中所述的概念[内核流式处理](kernel-streaming.md)。 有关创建适用于仅限音频设备，微型驱动程序信息[音频设备设计指南](https://docs.microsoft.com/windows-hardware/drivers/audio/index)。

通过 DVD、 MPEG 解码器、 视频解码器和调谐器，视频端口扩展 (VPEs) 和单个适配器上的音频编解码器的集成，支持所有这些设备和处理资源争用的统一的驱动程序模型简化了开发工作。

[AVStream](avstream-minidrivers-design-guide.md)并[Stream 类](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)这两个接口提供一个框架，为集成设备提供支持。 这些接口支持内核模式驱动程序之间的数据传输。 这些数据传输不需要线程转换为用户模式下，从而避免性能问题。

这两个接口支持流式处理模型的标准和自定义数据类型的统一。 Microsoft 定义了适用于大多数标准设备的属性集。 如果需要供应商可以提供其他属性集。

Microsoft 建议所有新的视频捕获驱动程序使用 AVStream 接口。 Microsoft 提供用于向后兼容性的 Stream 类接口。 但是，Stream 类接口已过时，并且 Microsoft 已停止使用其进一步开发。

**请注意**  :本部分不介绍已过时的视频的 Windows (VfW) 技术。 VfW 捕获到磁盘的电影进行了优化。 视频会议的重要功能，查看时，电视捕获视频字段和辅助数据流会丢失 VfW 体系结构。 若要避免这些限制，供应商已添加到 VfW 专有扩展插件。 但是，没有标准化接口的情况下使用这些功能的应用程序必须包含依赖于硬件的代码。
桥接 VfW 和 WDM 驱动程序模型，Microsoft 提供了一个 VfW WDM 映射器作为操作系统的一部分。 此组件使 WDM 驱动程序显示为 VfW 旧版 vfw，才能使用应用程序的驱动程序。

 

本部分包括：

[视频捕获概述](video-capture-overview.md)

[实现视频捕获支持](implementing-video-capture-support.md)

 

 




