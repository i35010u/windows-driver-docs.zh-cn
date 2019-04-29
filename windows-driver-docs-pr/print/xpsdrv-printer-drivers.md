---
title: XPSDrv 打印机驱动程序
description: XPSDrv 打印机驱动程序
ms.assetid: 9e61cb21-4e02-48dc-b291-576d37bb640d
keywords:
- XPSDrv 的打印机驱动程序 WDK，关于 XPS
- 打印机驱动程序 WDK XPSDrv
- XML 纸张规范 WDK 打印
- XPS 文档 WDK XPSDrv
- XPS 假脱机文件 WDK XPSDrv
- 打印后台打印文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c821b81b00cb315987fa849590330d432578fdb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390227"
---
# <a name="xpsdrv-printer-drivers"></a>XPSDrv 打印机驱动程序


XPSDrv 打印机驱动程序扩展了 Microsoft 的基于 GDI 的版本 3 打印机驱动程序体系结构以支持使用 XML 纸张规范 (XPS) 文档。 通过 XPSDrv 打印机驱动程序，XPS 文档格式可用作后台打印文件格式和文档文件格式。

### <a name="overview-of-xps"></a>XPS 的概述

XML 纸张规范 (XPS) 是用于文档和打印 Windows Vista 中的改进的基础。 本规范描述通过使用一种结构化的、 基于 XML 的文档格式的固定格式文档的外观。

XPS 文档格式包含 XML 标记定义文档的布局和显示或打印文档的呈现规则以及每个页面的可视外观。

### <a name="introduction-to-xps-for-printing"></a>用于打印为 XPS 简介

XPS 文档格式可作为一种文档格式、 后台打印文件格式和页面描述语言 (PDL) 的打印机。 如果您一直使用的是在整个文档周期 XPS，可以极大地提高打印可预见性和可靠性。 保真度和性能提高时文档格式是相同的作为后台打印文件格式和 PDL。 通过使用整个打印处理期间的 XPS 文档格式，可以无需应用程序和打印机之间的任何文档格式转换，以便您可以提供"所见即所得"(WYSIWYG) 体验。

XPS 假脱机文件使用 XPS 文档格式。 XPS 假脱机文件是开放并可扩展、 可通过使用的平台服务、 查看和可重新引入到文档的工作流。

XPS 假脱机文件来描述 XPS 文档中的标记适用于 Windows Presentation Foundation (WPF) 中的 Extensible Application Markup Language (XAML) 标记。 因此，XPS 假脱机文件中描述的文档可以呈现以本机方式在 WPF 中而不会丢失数据或保真度因为不不需要任何转换。 XPS 假脱机文件中的 XAML 标记是用于在 WPF 中的现有呈现类的 XAML 表示形式。 XPS 文档格式为"打印"的格式完全相同，并有效地保留应用程序内容和用户意向。

本部分包括：

[XPS 打印功能](xps-printing-features.md)

[Windows 打印路径概述](windows-print-path-overview.md)

[在早期版本的 Windows XP 支持](xps-support-in-earlier-versions-of-windows.md)

有关详细的打印机驱动程序开发人员的 XPS 打印有关的信息，请参阅[XPSDrv 的打印机驱动程序](xpsdrv-printer-driver.md)。
