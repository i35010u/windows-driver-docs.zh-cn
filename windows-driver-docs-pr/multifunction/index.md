---
title: 多功能设备驱动程序设计指南
description: 多功能设备驱动程序设计指南
ms.assetid: 110c0b9b-4870-4853-8fbf-a9faf0c5f2ca
keywords:
- 多功能设备 WDK
- 多功能设备 WDK, 关于多功能设备
- 组合功能设备 WDK
- 多功能设备 WDK
- 打印机多功能 WDK
- DVD/CD-ROM 多功能 WDK
- 多功能设备 WDK, 安装
- 父总线 WDK 多功能设备
- INF 文件 WDK 多功能设备
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 69588e8e53ad6872c779898765cc6ff15fa5059f
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223556"
---
# <a name="multifunction-device-driver-design-guide"></a>多功能设备驱动程序设计指南

一个多功能设备占用其父总线上的一个位置，但包含多个功能。 组合打印机/扫描仪/传真设备和调制解调器/网卡是常见的多功能设备。

在多功能设备中，各个功能是独立的。 这意味着这些功能必须具有以下特点：

- 这些功能不能依赖于启动顺序。

- 一个功能的资源要求不能通过另个一功能的资源来表述（例如，*function1* 使用 I/O 端口 *x*，*function2* 使用端口 *x* + 200）。

- 每个功能必须能够作为单独的设备运行，即使它与另一个功能由相同的驱动程序提供服务。

- 必须枚举设备上的每个功能。

- 每个功能的资源要求必须传达给 PnP 管理器。

- 每个功能都必须有 INF 文件和驱动程序。

负责每个此类任务的组件取决于设备的父总线的多功能标准、在多大程度上设备必须符合该标准，以及父总线驱动程序的功能。

如果设备遵循其总线的多功能标准，则驱动程序要求会显著减少。 已经为电脑卡和 PCI 总线定义行业范围的多功能标准。

如果要使用用于数据存储（不用于音频/视频播放）的多功能 DVD/CD-ROM 设备，则应使用系统提供的 WDM DVD 类驱动程序，后者将设备视为单个逻辑单元。

对于组合了其他功能的多功能设备，如果设备遵循其总线的多功能标准，则可使用系统提供的驱动程序和 INF 文件。 系统提供的多功能驱动程序 (mf.sys) 可以处理针对设备的总线级别枚举和资源分配要求，而系统提供的 INF (mf.sys) 则可安装多功能设备。 对于各个设备功能，只需提供一个功能驱动程序和 INF 文件。

如果设备不遵循其总线的标准，则除了适用于设备功能的功能驱动程序和 INF 文件，可能还需要提供在功能上等效于 mf.sys 的驱动程序。

若要安装多功能设备，通常需提供一个适用于设备的基础 INF 文件，另外再提供一个适用于设备的每个功能的 INF 文件。 基础 INF 文件通常复制适用于设备的各个功能的 INF 文件。 若要了解如何完成此任务，请参阅[复制 INF](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)。

以下部分介绍各类多功能设备的驱动程序和安装要求：

[支持多功能电脑卡设备](supporting-multifunction-pc-card-devices.md)

[支持多功能 PCI 设备](supporting-multifunction-pci-devices.md)

[支持其他总线上的多功能设备](supporting-multifunction-devices-on-other-buses.md)

[使用系统提供的多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md)

[为多功能设备创建资源映射](creating-resource-maps-for-a-multifunction-device.md)

有关 INF 文件语法的信息，请参阅 [INF File Sections and Directives](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)（INF 文件节和指令）。

Windows 驱动程序工具包 (WDK) 包括一个单独的部分，介绍如何支持[多功能音频设备](https://docs.microsoft.com/windows-hardware/drivers/audio/multifunction-audio-devices)。
