---
title: 自定义音频驱动程序
description: 自定义音频驱动程序
ms.assetid: d5f19a72-0b43-4fe1-b0e1-0198344b4d19
keywords:
- WDM 音频驱动程序 WDK，自定义
- 音频驱动程序 WDK，自定义
- 自定义音频驱动程序 WDK
- 供应商提供的驱动程序 WDK 音频
- PortCls WDK 音频，自定义音频驱动程序
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: f8eceead615c1e7fdf9f1b0e9b95e285b03ec34b
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925602"
---
# <a name="custom-audio-drivers"></a>自定义音频驱动程序


不 UAA 兼容的音频设备需要供应商提供的自定义驱动程序。 此外，UAA 兼容的音频适配器可包含 UAA 类驱动程序不支持的专有功能;仅当供应商提供自定义音频驱动程序时，应用程序才可以访问这些功能。 只有标准 UAA 功能可通过系统提供的 UAA 驱动程序进行访问。 有关 UAA 支持的功能的信息，请参阅[通用音频体系结构](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn640534(v=vs.85))白皮书。

硬件供应商可以使用两个选项来编写自定义音频驱动程序：开发用于 PortCls 系统驱动程序（Portcls）的自定义音频适配器驱动程序，或开发用于 AVStream 类系统驱动程序（Ks）的自定义微型驱动程序。

大多数自定义音频适配器驱动程序使用 PortCls，它是操作系统的一部分提供的。 PortCls 系统驱动程序（Portcls）包含内置的音频驱动程序基础结构，使编写自定义音频驱动程序的任务更容易。 PortCls 实现了多个端口驱动程序，其中每个驱动程序都专用于管理特定类型的波形、MIDI 或混音设备的一般功能。 选择一组合适的端口驱动程序来管理音频适配器上的音频功能后，供应商开发一组互补的微型端口驱动程序，该驱动程序与所选端口驱动程序一起工作，并控制音频设备的硬件相关功能。

供应商还可以通过开发自定义的 AVStream 类微型驱动程序来支持音频设备。 微型驱动程序与 AVStream 类系统驱动程序一起工作，该驱动程序是作为操作系统的一部分提供的。 实现 AVStream 驱动程序比使用 PortCls 更难，但这样做可能仍适用于集成音频和视频的设备。 对于不符合系统提供的 USBAudio 或 AVCAudio 类系统驱动程序要求的现有 USB 或 IEEE 1394 音频设备，也可能需要 AVStream 驱动程序。

对于几乎所有需要供应商提供的自定义驱动程序的 PCI 音频适配器，供应商应选择 "PortCls"。

AVStream 类系统驱动程序（Ks）缺少 PortCls 中存在的大多数特定于音频的支持函数。

有关 PortCls 的详细信息，请参阅[Port Class 简介](introduction-to-port-class.md)。 有关 AVStream 的详细信息，请参阅[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)。

 

 




