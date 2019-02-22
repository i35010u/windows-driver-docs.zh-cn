---
title: XPS 筛选器
description: XPS 筛选器
ms.assetid: dd8044a6-6558-488e-9508-a83718fabb7d
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv XPS 筛选器
- XPS 筛选 WDK XPSDrv
- DllGetClassObject
- WDK XPS 的筛选器
- IPrintPipelineFilter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba5075a0d09a710cb670e362c21008f513997b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544419"
---
# <a name="xps-filters"></a>XPS 筛选器


有关 XPS 打印路径，筛选器是一个驱动程序用于为打印机准备打印的数据的主要方法。 在 Windows Vista 之前的 Microsoft Windows 操作系统版本中，打印处理器和呈现模块进行了筛选器的工作。

XPS 筛选器是导出的 DLL [DllGetClassObject](https://go.microsoft.com/fwlink/p/?linkid=123418)并[DllCanUnloadNow](https://go.microsoft.com/fwlink/p/?linkid=123419)函数。 它加载和卸载 XPS 筛选器 DLL 时，筛选器管道管理器将调用这些函数。 加载筛选器 DLL 后, 筛选器管道管理器执行以下任务：

-   调用**DllGetClassObject**若要获取对筛选器对象的引用[IClassFactory](https://go.microsoft.com/fwlink/p/?linkid=123420)接口。

-   调用[IClassFactory::CreateInstance](https://go.microsoft.com/fwlink/p/?linkid=123421)方法来获取对筛选器对象的引用[IPrintPipelineFilter](https://msdn.microsoft.com/library/windows/hardware/ff554286)接口。

-   调用[ **IPrintPipelineFilter::InitializeFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff554291)方法来初始化筛选器对象。

卸载前倒带筛选器 DLL，该筛选器管道管理器调用**DllCanUnloadNow**。

**请注意**  在某些较旧的 XPS 筛选器， **DllGetClassObject**函数将检索到的筛选器的引用**IPrintPipelineFilter** 而不是接口**IClassFactory**接口。 为了向后兼容，Windows Vista 和更高版本的 Windows 中的筛选器管道管理器将继续支持这些筛选器。 但是，对于新的筛选器设计**DllGetClassObject**应检索到的引用**IClassFactory**接口。



XPS 筛选器会使打印子系统更加可靠，因为筛选器不同于后台处理程序的进程中运行。 此"沙盒"同时可避免失败，并允许插件使用不同的安全权限来运行。 XPSDrv 还可以在打印机来降低成本和开发时间系列中重复使用筛选器。

有关最大的灵活性和重复使用，每个筛选器应执行的特定打印处理函数。 例如，一个筛选器仅会应用水印，而另一个仅可进行记帐。

Windows Vista 不包括任何筛选器中的框中，但以下示例筛选器包括在 Windows 驱动程序工具包 (WDK) 中\\Src\\打印\\Xpsdrvsmpl\\Src\\筛选器文件夹：

-   手册

-   颜色转换

-   Nup

-   页面缩放方式

-   水印

有关筛选器管道管理器的详细信息，请参阅[XPSDrv 呈现模块](xpsdrv-render-module.md)。

有关实现筛选器的详细信息，请参阅[实现 XPS 筛选器](implementing-xps-filters.md)。

有关打印筛选器中的异步通知的详细信息，请参阅[打印筛选器中的异步通知](asynchronous-notifications-in-print-filters.md)。

必须使用配置筛选器[筛选器管道配置文件](filter-pipeline-configuration-file.md)。

有关如何调试打印筛选器管道服务的信息，请参阅[将调试器附加到打印筛选器管道服务](attaching-a-debugger-to-the-print-filter-pipeline-service.md)。

在 Windows 7 中，可以使用 XPS 筛选器[XPS 光栅化服务](using-the-xps-rasterization-service.md)将转换为位图的 XPS 文档中的固定的页。

有关 Windows 的方式的信息为 XPS 光栅化使用 GPU 加速，请参阅[XPSRas GPU 使用情况决策树](xpsras-usage-decision-tree.md)。

