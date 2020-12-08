---
title: XPSDrv 打印机驱动程序
description: XPSDrv 打印机驱动程序
keywords:
- XPSDrv 打印机驱动程序 WDK，关于 XPS
- 打印机驱动程序 WDK，XPSDrv
- XML 纸张规范 WDK 打印
- XPS 文档 WDK XPSDrv
- XPS 假脱机文件 WDK XPSDrv
- 假脱机文件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 273cceea40ae1aee9e8b8a6c434ebb1000dd476f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785693"
---
# <a name="xpsdrv-printer-drivers"></a>XPSDrv 打印机驱动程序


XPSDrv 打印机驱动程序扩展了 Microsoft 的基于 GDI 的版本3打印机驱动程序体系结构，以支持使用 XML 纸张规范 (XPS) 文档。 通过 XPSDrv 打印机驱动程序，XPS 文档格式可用作后台打印文件格式和文档文件格式。

### <a name="overview-of-xps"></a>XPS 概述

 (XPS) 的 XML 纸张规范是 Windows Vista 中的文档和打印改进的基础。 此规范使用基于 XML 的结构化文档格式描述固定格式文档的外观。

XPS 文档格式由定义文档布局的 XML 标记和每个页面的视觉外观以及显示或打印文档的呈现规则组成。

### <a name="introduction-to-xps-for-printing"></a>XPS 打印简介

XPS 文档格式作为文档格式、假脱机文件格式，以及 (PDL) 用于打印机的页面描述语言。 如果在整个文档周期中一直使用 XPS，则可以极大地提高打印可预测性和可靠性。 如果文档格式与假脱机文件格式和 PDL 相同，则保真度和性能会提高。 通过在整个打印处理中使用 XPS 文档格式，您可以无需在应用程序和打印机之间进行任何文档格式转换，因此您可以提供 "所见即所得内容" (WYSIWYG) 体验。

XPS 假脱机文件使用 XPS 文档格式。 XPS 假脱机文件是开放且可扩展的，可以通过使用平台服务进行查看，并且可以重新引入到文档工作流中。

用于描述 XPS 文档的 XPS 假脱机文件中的标记与 Windows Presentation Foundation (WPF) 中的 Extensible Application Markup Language (XAML) 标记兼容。 因此，在没有数据或保真度损失的情况下，XPS 假脱机文件中描述的文档可以在 WPF 中以本机方式呈现，因为无需进行任何转换。 XPS 假脱机文件中的 XAML 标记是 WPF 中现有呈现类的 XAML 表示形式。 XPS 文档格式与 "打印" 格式相同，并有效地保留应用程序内容和用户意向。

本节包括：

[XPS 打印功能](xps-printing-features.md)

[Windows 打印路径概述](windows-print-path-overview.md)

[早期 Windows 版本中的 XPS 支持](xps-support-in-earlier-versions-of-windows.md)

有关打印机驱动程序开发人员的 XPS 打印的更多详细信息，请参阅 [XPSDrv 打印机驱动程序](xpsdrv-printer-driver.md)。
