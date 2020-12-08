---
title: XPSDrv 配置模块
description: XPSDrv 配置模块
keywords:
- XPSDrv 打印机驱动程序 WDK，配置模块
- 配置模块 WDK XPSDrv，关于配置模块
- 转换呈现模块 WDK XPSDrv
- 通知 WDK XPSDrv
- 事件通知 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff2298f31be35f385e4f8a16c0b61a5abb21ea94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785731"
---
# <a name="xpsdrv-configuration-module"></a>XPSDrv 配置模块


XPSDrv 打印驱动程序是 XPS 打印路径的组件，它使用 XPS 假脱机文件，并发出页面描述语言 (可供打印机使用的 PDL) 数据。 配置模块包含驱动程序组件，这些组件将打印机功能和设置与应用程序进行通信。 XPSDrv 打印机驱动程序支持基于 Microsoft Win32 的应用程序和 Windows Presentation Foundation (基于 WPF) 的应用程序使用的通信方法。

基于 Win32 的应用程序和 WPF 应用程序都可以打印到 XPSDrv 打印驱动程序。 Win32 应用程序 (API) 使用 GDI 打印应用程序编程接口，而 Microsoft 提供的转换呈现模块会创建一个 XPS 假脱机文件，用于打印到打印筛选器管道。 WPF 应用程序使用 WPF 打印 API 直接从应用程序创建 XPS 假脱机文件。

下图显示了 XPSDrv 配置体系结构。

![说明 xpsdrv 配置体系结构的关系图](images/xpsconfig.png)

请注意，配置模块部分中的三个对象是相互排斥的。

XPSDrv 打印驱动程序的两个主要组件是 [版本3打印驱动程序模块](version-3-xpsdrv-print-driver-components.md) 和 [XPS 筛选器管道](filter-pipeline-configuration-file.md)。 其中每个组件都需要一个或多个配置文件和模块。

### <a name="xpsdrv-document-events"></a>XPSDrv 文档事件

如果在将基于 Win32 的应用程序打印到时，XPSDrv 驱动程序可以通过 [**DrvDocumentEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentevent) 函数接收 GDI 文档事件，并且驱动程序可以通过 DRVDOCUMENTEVENT 在 WPF 应用程序打印时接收 XPS 文档事件。 有关 XPSDrv 文档事件的详细信息，请参阅 [Xpsdrv 驱动程序文档事件](xps-driver-document-events.md)。

### <a name="xpsdrv-driver-installation"></a>XPSDrv 驱动程序安装

XPSDrv 驱动程序具有特定的安装要求。 有关 XPSDrv 驱动程序安装的详细信息，请参阅 [Xpsdrv 安装](xpsdrv-installation.md)。

 

