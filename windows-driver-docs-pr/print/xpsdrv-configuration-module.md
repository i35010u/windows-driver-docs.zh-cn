---
title: XPSDrv 配置模块
description: XPSDrv 配置模块
ms.assetid: 439d7769-57d1-41f9-a3db-da254b4b7cae
keywords:
- XPSDrv 的打印机驱动程序 WDK，配置模块
- 配置模块 WDK XPSDrv 配置模块的相关
- 转换呈现模块 WDK XPSDrv
- 通知 WDK XPSDrv
- 事件通知 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d50343abebb3690d191699f89b035089468be6aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363371"
---
# <a name="xpsdrv-configuration-module"></a>XPSDrv 配置模块


XPSDrv 打印机驱动程序是使用 XPS 假脱机文件并发出可以使用打印机的页面描述语言 (PDL) 数据的 XPS 打印路径组件。 配置模块包含打印机功能和设置应用于应用程序进行通信的驱动程序组件。 XPSDrv 的打印机驱动程序支持 Microsoft 基于 Win32 的应用程序和-基于 Windows Presentation Foundation (WPF） 应用程序使用的通信方法。

基于 Win32 的应用程序和 WPF 应用程序都可以打印到 XPSDrv 打印驱动程序。 Win32 应用程序使用 GDI 打印应用程序编程接口 (API) 和 Microsoft 提供转换呈现模块创建 XPS 假脱机文件以供打印到打印筛选器管道。 WPF 应用程序使用 WPF 打印 API 直接从应用程序创建 XPS 假脱机文件。

下图显示了 XPSDrv 配置体系结构。

![说明 xpsdrv 配置体系结构的关系图](images/xpsconfig.png)

请注意，配置模块部分中的三个对象相互排斥。

XPSDrv 打印机驱动程序的两个主要组件包括[版本 3 打印驱动程序模块](version-3-xpsdrv-print-driver-components.md)并[XPS 筛选器管道](filter-pipeline-configuration-file.md)。 每个组件需要一个或多个配置文件和模块。

### <a name="xpsdrv-document-events"></a>XPSDrv 文档事件

XPSDrv 驱动程序可以接收通过 GDI 文档事件[ **DrvDocumentEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)时基于 Win32 的应用程序要打印到它们，并将驱动程序可以接收通过 XPS 文档事件的功能DrvDocumentEvent WPF 应用程序打印到它们时。 有关 XPSDrv 文档事件的详细信息，请参阅[XPSDrv 驱动程序文档事件](xps-driver-document-events.md)。

### <a name="xpsdrv-driver-installation"></a>XPSDrv 驱动程序安装

XPSDrv 驱动程序已安装的特定要求。 有关 XPSDrv 驱动程序安装的详细信息，请参阅[XPSDrv 安装](xpsdrv-installation.md)。

 

 




