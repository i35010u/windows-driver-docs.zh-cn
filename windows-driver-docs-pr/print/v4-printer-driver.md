---
title: V4 打印机驱动程序
description: v4 打印机驱动程序模型旨在解决版本 3 驱动程序模型中的已知问题，从而提高用户使用打印机的体验质量。
ms.date: 04/20/2017
ms.localizationpriority: high
ms.openlocfilehash: b82621c6e9950cdbcee3473538d78d16ed82f12e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785875"
---
# <a name="v4-printer-driver"></a>V4 打印机驱动程序


v4 打印机驱动程序模型旨在解决版本 3 驱动程序模型中的已知问题，从而提高用户使用打印机的体验质量。

**注意** 为了帮助更好地解释本部分中的一些概念，我使用了一家名为 Fabrikam 的虚构公司。

 

**简介**

v4 打印机驱动程序模型是对现有 v3 打印机驱动程序模型的优化，旨在改进驱动程序开发、降低 IT 管理成本，并支持新的方案。 v4 打印机驱动程序模型继续支持许多熟悉的技术，例如 [XPSDrv](xpsdrv-printer-driver.md)、[GPD](introduction-to-gpd-files.md)、[PPD](pscript-minidrivers.md)、[Autoconfiguration](printer-autoconfiguration.md) 和 [Bidi](bidirectional-communication.md)。 v4 打印机驱动程序模型还支持多个新的扩展点。

v4 打印机驱动程序模型还针对几种新的方案进行了优化，其中包括：

-   Windows 8 方案

    UWP 应用提出了有关 UI 行为和安全上下文的新设计注意事项。 因此，需要一个打印机驱动程序模型，这将为此新环 境提供深度集成支持。 v4 打印机驱动程序模型为打印机制造商提供了在 UWP 应用中提供自定义“打印首选项”体验或“打印机通知”体验的唯一方法。

-   打印机共享

    打印机共享是 Windows Server 的关键价值主张项。 v4 打印机驱动程序模型旨在通过消除跨处理器体系结构管理驱动程序的需求，使共享变得更加轻松和高效。

-   易于驱动程序开发

    v4 驱动程序必须支持版本 3 打印机驱动程序模型和 XPSDrv 体系结构中的现有开发工作。 而且，v4 驱动程序必须更易于开发和测试。

**概要体系结构**

下面是 v4 打印机驱动程序的概要表示形式。 除了渲染筛选器和用户界面应用程序之外，关系图中的所有其他功能块均由 Microsoft 实现。 V4 打印机驱动程序在很大程度上依赖于数据文件和 JavaScript 来实现扩展性。 蓝色框表示在 v3 驱动程序模型中使用的现有文件，而绿色框表示插入的新位置。

![v4 打印机驱动程序的概要表示形式](images/v4driverarch.png)

本节内容讨论了 v4 打印机驱动程序的以下方面：

[V4 打印机驱动程序渲染](v4-driver-rendering.md)

[V4 打印机驱动程序配置](v4-driver-configuration.md)

[V4 打印机驱动程序安装](v4-driver-setup.md)

[V4 打印机驱动程序用户界面](v4-printer-driver-user-interfaces.md)

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)

[在 Visual Studio 中生成 v4 打印机驱动程序](build-a-v4-print-driver-in-visual-studio.md)

 

 




