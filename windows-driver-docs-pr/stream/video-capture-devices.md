---
title: 视频捕获设备
description: 视频捕获设备
keywords:
- 捕获视频 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa1ed581238413a205b4ae937bc99a3019a25140
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783717"
---
# <a name="video-capture-devices"></a>视频捕获设备


本部分介绍如何创建视频捕获微型驱动程序，它遵循 Windows 驱动模型 (WDM) 体系结构。 它假定你熟悉 [内核流](kernel-streaming.md)中所述的概念。 有关创建仅音频设备的微型驱动程序的信息，请查看 [音频设备设计指南](../audio/index.md)。

集成 DVD、MPEG 解码器、视频解码器和调谐器、视频端口扩展 (VPEs) ，以及单个适配器上的音频编解码器，这是一个统一的驱动程序模型，支持所有这些设备并处理资源争用，从而简化了开发工作。

[AVStream](avstream-minidrivers-design-guide.md)和[Stream 类](/windows-hardware/drivers/ddi/_stream/index)接口都提供一个框架，该框架提供对集成设备的支持。 这些接口支持内核模式驱动程序之间的数据传输。 这些数据传输不需要线程转换为用户模式，从而避免了性能下降。

这两个接口都支持标准和自定义数据类型的统一流式处理模型。 Microsoft 为大多数标准设备定义了属性集。 如果需要，供应商可以提供其他属性集。

Microsoft 建议所有新视频捕获驱动程序都使用 AVStream 接口。 Microsoft 为提供向后兼容性提供流类接口。 但是，流类接口已过时，并且 Microsoft 已不再进行进一步的开发。

**注意**  ：本部分不介绍 Windows (VfW) 技术的过时视频。 VfW 已针对捕获电影到磁盘进行了优化。 VfW 体系结构中缺少对视频会议、电视观看、视频字段捕获和辅助数据流的重要功能。 为了规避这些限制，供应商已将专有扩展添加到 VfW。 但是，如果没有标准化接口，使用这些功能的应用程序必须包含硬件相关的代码。
为了桥接 VfW 和 WDM 驱动程序模型，Microsoft 提供了 VfW 映射器作为操作系统的一部分。 此组件启用 WDM 驱动程序，使其作为旧版 VfW 应用程序的 VfW 驱动程序。

 

本节包括：

[视频捕获概述](video-capture-overview.md)

[实现视频捕获支持](implementing-video-capture-support.md)

 

