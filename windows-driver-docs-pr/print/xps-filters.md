---
title: XPS 筛选器
description: XPS 筛选器
ms.assetid: dd8044a6-6558-488e-9508-a83718fabb7d
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，XPS 筛选器
- XPS 筛选器 WDK XPSDrv
- DllGetClassObject
- 筛选 WDK XPS
- IPrintPipelineFilter
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 64169a01f28736f62785c02bf5f910ec37e0719b
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793741"
---
# <a name="xps-filters"></a>XPS 筛选器

对于 XPS 打印路径，筛选器是驱动程序为打印机准备打印数据的主要方式。 在 Windows Vista 之前的 Microsoft Windows 操作系统版本中，打印处理器和呈现模块执行筛选器工作。

XPS 筛选器是导出[DllGetClassObject](https://go.microsoft.com/fwlink/p/?linkid=123418)和[DLLCANUNLOADNOW](https://go.microsoft.com/fwlink/p/?linkid=123419)函数的 DLL。 在加载和卸载 XPS 筛选器 DLL 时，筛选器管道管理器会调用这些函数。 在加载筛选器 DLL 之后，筛选器管道管理器将执行以下操作：

- 调用**DllGetClassObject**以获取对筛选器对象的[IClassFactory](https://go.microsoft.com/fwlink/p/?linkid=123420)接口的引用。

- 调用[IClassFactory：： CreateInstance](https://go.microsoft.com/fwlink/p/?linkid=123421)方法以获取对筛选器对象的[IPrintPipelineFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelinefilter)接口的引用。

- 调用[**IPrintPipelineFilter：： InitializeFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nf-filterpipeline-iprintpipelinefilter-initializefilter)方法以初始化筛选器对象。

在卸载筛选器 DLL 之前，筛选器管道管理器调用**DllCanUnloadNow**。

> [!NOTE]
> 在一些较旧的 XPS 筛选器中， **DllGetClassObject**函数检索对筛选器的**IPrintPipelineFilter**接口而不是**IClassFactory**接口的引用。 为了向后兼容，Windows Vista 和更高版本的 Windows 中的筛选器管道管理器将继续支持这些筛选器。 但是，对于新的筛选器设计， **DllGetClassObject**应检索对**IClassFactory**接口的引用。

XPS 筛选器使打印子系统更可靠，因为筛选器在与后台处理程序不同的进程中运行。 这种 "沙盒处理" 可防止出现故障，并允许插件以不同的安全权限运行。 使用 XPSDrv，还可以在打印机系列之间重复使用筛选器，从而降低成本和开发时间。

为了最大限度地提高灵活性和重复使用，每个筛选器都应执行特定的打印处理功能。 例如，一个筛选器将仅应用水印，而另一个筛选器只会执行记帐。

Github 上提供了以下[XPS 驱动程序和筛选器示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/xpsdrv-driver-and-filter-sample/)：

- 手册

- 颜色转换

- Nup

- 页面缩放

- 水印

有关筛选器管道管理器的详细信息，请参阅[XPSDrv Render Module](xpsdrv-render-module.md)。

有关实现筛选器的详细信息，请参阅[实现 XPS 筛选器](implementing-xps-filters.md)。

有关打印筛选器中的异步通知的详细信息，请参阅[打印筛选器中的异步通知](asynchronous-notifications-in-print-filters.md)。

必须使用[筛选器管道配置文件](filter-pipeline-configuration-file.md)配置筛选器。

有关如何调试打印筛选器管道服务的信息，请参阅将[调试器附加到打印筛选器管道服务](attaching-a-debugger-to-the-print-filter-pipeline-service.md)。

在 Windows 7 中，XPS 筛选器可以使用[xps 光栅化服务](using-the-xps-rasterization-service.md)将 xps 文档中的固定页面转换为位图。

有关 Windows 使用 XPS 光栅化的 GPU 加速方式的信息，请参阅[XPSRAS GPU 使用情况决策树](xpsras-usage-decision-tree.md)。
