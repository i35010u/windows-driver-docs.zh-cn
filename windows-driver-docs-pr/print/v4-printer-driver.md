---
title: V4 打印机驱动程序
description: V4 打印机驱动程序模型旨在解决的已知问题的版本 3 驱动程序模型，并因此改进的用户在他们的打印机的体验质量。
ms.assetid: CB333340-FBA0-4CB4-BAD6-4673B4AC0DF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce43f9ca4b8d3ae71c9ef56bc8ae8513186dc50a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567019"
---
# <a name="v4-printer-driver"></a>V4 打印机驱动程序


V4 打印机驱动程序模型旨在解决的已知问题的版本 3 驱动程序模型，并因此改进的用户在他们的打印机的体验质量。

**请注意**  为了帮助更好地介绍一些在本部分中的概念，请使用名为 Fabrikam 的虚构公司。

 

**简介**

V4 打印机驱动程序模型是现有的 v3 打印机驱动程序模型的优化，它旨在改进驱动程序开发，降低 IT 管理成本，并支持新方案。 V4 打印驱动程序模型仍支持许多熟悉的技术，如[XPSDrv](xpsdrv-printer-driver.md)， [GPD](introduction-to-gpd-files.md)， [PPD](pscript-minidrivers.md)，[自动配置](printer-autoconfiguration.md)，和[Bidi](bidirectional-communication.md)。 V4 打印驱动程序模型还支持多个新的扩展点。

V4 打印驱动程序模型也适用于几个新方案，其中包括：

-   Windows 8 方案

    UWP 应用程序可提供有关 UI 行为和安全上下文的新设计注意事项。 因此，需要使用打印机驱动程序模型是这样就为此新环境提供深度集成的支持。 V4 打印驱动程序模型提供了打印机制造商提供自定义打印首选项的唯一方式体验或打印机通知体验在 UWP 应用中。

-   打印机共享

    打印机共享是 Windows 服务器的密钥值主张项。 V4 打印机驱动程序模型旨在使共享更轻松、 更高效，无需跨处理器体系结构中管理驱动程序。

-   易用性驱动程序开发

    V4 驱动程序必须支持从版本 3 的打印机驱动程序模型和 XPSDrv 体系结构的现有开发工作。 并且还，v4 驱动程序必须是更轻松地开发和测试。

**高级体系结构**

下面是 v4 打印驱动程序的高水平表现。 除了呈现筛选器和用户界面应用程序中，所有其他功能块在关系图中由 Microsoft 实现。 V4 打印驱动程序依赖于数据文件和 JavaScript 可扩展性。 蓝色框表示的 v3 驱动程序模型中使用了现有文件和绿色框表示要插入的新位置。

![v4 打印驱动程序的高级别的表示形式](images/v4driverarch.png)

本部分讨论 v4 打印机驱动程序的以下方面：

[V4 打印机驱动程序呈现](v4-driver-rendering.md)

[V4 打印机驱动程序配置](v4-driver-configuration.md)

[V4 打印机驱动程序安装程序](v4-driver-setup.md)

[V4 打印机驱动程序的用户界面](v4-printer-driver-user-interfaces.md)

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)

[生成 Visual Studio 中的 v4 打印机驱动程序](build-a-v4-print-driver-in-visual-studio.md)

 

 




