---
title: 自定义音频驱动程序
description: 自定义音频驱动程序
ms.assetid: d5f19a72-0b43-4fe1-b0e1-0198344b4d19
keywords:
- WDM 音频驱动程序 WDK，自定义
- 音频驱动程序 WDK，自定义
- 自定义的音频驱动程序 WDK
- 供应商提供的驱动程序 WDK 音频
- PortCls WDK 音频、 自定义音频驱动程序
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19bc9a0027326fb44a2b1aa56708849f58471e9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359108"
---
# <a name="custom-audio-drivers"></a>自定义音频驱动程序


不能 UAA 兼容的音频设备需要供应商提供自定义驱动程序。 此外，UAA 兼容音频适配器可以合并 UAA 类驱动程序; 不支持的专有功能仅当供应商提供的自定义的音频驱动程序，这些功能都可以访问应用程序。 仅标准 UAA 功能是可通过系统提供 UAA 驱动程序访问。 UAA 支持的功能有关的信息，请参阅[通用音频体系结构](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc)白皮书。

两个选项可供硬件供应商编写自定义音频驱动程序： 开发的自定义音频适配器驱动程序使用与 PortCls 系统驱动程序 (Portcls.sys)，或开发自定义的微型驱动程序，以用于 AVStream 类系统驱动程序 (Ks.sys).

大多数自定义驱动程序，为音频适配器使用 PortCls，作为操作系统的一部分提供。 PortCls 系统驱动程序 (Portcls.sys) 包含了内置的音频驱动程序基础结构，使编写的自定义的音频驱动程序更轻松的任务。 PortCls 实现多个端口驱动程序，其中每个专用于管理特定类型的批、 MIDI 或混音器设备的泛型函数。 选择后一组适当的端口驱动程序来管理音频适配器上的音频函数，供应商开发互补一系列可与所选的端口驱动程序结合和控制的依赖于硬件的功能的微型端口驱动程序音频设备。

供应商还可以通过开发自定义 AVStream 类微型驱动程序支持的音频设备。 微型驱动程序结合 AVStream 类系统驱动程序，它提供作为操作系统的一部分工作。 实现 AVStream 驱动程序难度大于使用 PortCls，但这样做因此仍可能适用的设备的音频和视频集成。 AVStream 驱动程序也可能有必要的现有 USB 或 IEEE 1394 音频设备无法符合系统提供 USBAudio 或 AVCAudio 类系统驱动程序的要求。

对于几乎所有 PCI 音频适配器所需供应商提供自定义驱动程序，供应商应选择 PortCls。

AVStream 类系统驱动程序 (Ks.sys) 缺少大部分 PortCls 中存在的特定于音频的支持函数。

有关 PortCls 详细信息，请参阅[简介端口类](introduction-to-port-class.md)。 有关 AVStream 详细信息，请参阅[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)。

 

 




