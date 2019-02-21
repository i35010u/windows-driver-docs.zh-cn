---
title: OpenXPS 的驱动程序支持
description: OpenXPS 是文档的 Open XML 纸张规范格式和基于 Ecma 国际标准规范。
ms.assetid: 9BC9787E-A54D-4A11-B256-57BE5D206404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b3d16238e3ad8da131a4748e0487acc07006df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540496"
---
# <a name="driver-support-for-openxps"></a>OpenXPS 的驱动程序支持


OpenXPS 是文档的 Open XML 纸张规范格式和基于 Ecma 国际标准规范。

有关此规范的日期信息的最，请参阅[Open XML 纸张规范](http://www.ecma-international.org/publications/standards/Ecma-388.htm)。

Windows 8 提供完全支持 OpenXPS，继续支持现有的 Microsoft XPS 格式与并行。 本主题着重于 OpenXPS 支持通过 v4 驱动程序模型。 与 Windows 应用程序开发人员相关的 OpenXPS 支持，请参阅[OpenXPS 打印应用程序支持](https://msdn.microsoft.com/library/windows/desktop/dn495653.aspx)。

## <a name="supported-openxps-scenarios"></a>支持的 OpenXPS 方案


Windows 打印路径已开发以确保提交的 XPS 格式匹配的目标的打印驱动程序，受支持的格式，并根据需要将转换格式。 Windows 还提供 Api 来查询打印驱动程序，以便应用程序可以提供兼容的元素，并避免在打印系统中的任何其他转换。

打印驱动程序可以使用其清单以指示它是否支持 Microsoft XPS、 打开 XPS 或这两种格式。 Microsoft XPS 或 OpenXPS 可以提供给打印筛选器管道中的筛选器，使用现有的流和对象模型 (OM) 接口 – 任何新接口所需的驱动程序支持 OpenXPS。 向筛选器中显示的格式取决于驱动程序，支持的格式或应用程序提供的格式。

已更新 Microsoft XPS 文档编写器 (MXDW) 以允许从任何 Windows 桌面应用程序输出 Microsoft XPS 或 OpenXPS MXDW。 同样，Microsoft XPS 查看器和 Windows 8 中的读取器应用程序可以打开这两种 XPS 格式。 如果需要用户可以从打印 XPS 查看器到 MXDW 换算格式。

## <a name="unsupported-openxps-scenarios"></a>不支持的 OpenXPS 方案


某些旧的功能不受支持，或提供降级的体验与 OpenXPS 一起使用时。

*不支持*:OpenXPS 文件将直接发送到后台处理程序 （跳过 XPS 打印 API） 是一个不受支持的方案。 执行此操作，将生成以下功能问题：

-   XPS 假脱机文件直接发送到后台处理程序将视为 MSXPS 并进行相应处理。
-   OpenXPS 文件将直接发送到后台处理程序的结果是不确定，并可能会导致打印作业失败。

**请注意**  没有计划为此方案提供支持。

 

*不建议这样做*:发送 OpenXPS 直接到 XPS 打印 API 的应用程序中的流不是推荐的方法。 例如，不要直接向 StartXPSPrintJob 方法发送的 OpenXPS 流。 如果这样做，生成转换从一种风格，XPS 的另一个流的形式可以是非常高的性能。

相反，应使用 IPrintDocumentPackageTarget 提交打印作业作为 XPS OM 以避免性能降低。

*不建议这样做*:XPS 假脱机文件将直接发送到后台处理程序。 如果这样做，打印系统将不到由打印路径 Api 添加所需的元数据，假定格式 MSXPS，并且将尝试将其转换为 OpenXPS。 如果直接发送给后台处理程序的假脱机文件的 OpenXPS 格式的文件，将其转换为 OpenXPS 打印筛选器管道的尝试将结果不确定。 如果已发送到后台处理程序的文件是一个 MSXPS 格式的文件和驱动程序是仅限 OpenXPS 的驱动程序，到 OpenXPS 的打印筛选器管道转换会成功。 但此后期阶段转换会导致打印系统性能显著降低。

## <a name="impact-on-app-developers"></a>对应用程序开发人员的影响


OpenXPS 的 Windows 8 支持的应用程序开发人员影响信息，请参阅[OpenXPS 打印应用程序支持](https://msdn.microsoft.com/library/windows/desktop/dn495653.aspx)。

## <a name="impact-on-driver-developers"></a>对驱动程序开发人员的影响


在 v4 打印驱动程序中启用 OpenXPS 的基本步骤如下：

-   驱动程序清单：将"OpenXPS"添加到驱动程序呈现部分。
-   驱动程序清单：如果适用，将"oxps"添加到存部分。
-   筛选器管道：更新用于处理 OpenXPS 元素的打印筛选器。

对于给定的流，以及合适的对象接口，客户端可以使用 OpenXPS 格式将数据传输到的打印筛选器管道中的筛选器。 若要传输的数据流，客户端使用 IID\_IPrintReadStream 和 IID\_IPrintWriteStream 接口。 若要将数据传输到 OM 组件，客户端使用 IID\_IXpsDocumentProvider 和 IID\_IXpsDocumentConsumer 接口。 声明对 OpenXPS 支持的驱动程序将需要确保提供的打印筛选器可以正确地处理 OpenXPS 格式，当从管道管理器收到此格式。

**驱动程序清单：DriverRender 部分**。 驱动程序在安装期间，安装过程检查清单 XpsFormat 条目是否包括 OpenXPS DriverRender 部分。 XpsFormat 条目可以包括 XPS （适用于 Microsoft XPS) 和 OpenXPS，以指示双支持。 在这两种格式列出 XpsFormat 条目中的顺序确定驱动程序的首选的格式。

以下是如何更新 DriverRender 节的一些示例。

指示仅支持 OpenXPS:

```Manifest
[DriverRender]
XpsFormat = OpenXPS
```

指示仅支持 MSXPS:

```Manifest
[DriverRender]
XpsFormat = XPS
```

该值指示通过 OpenXPS 的首选项这两种格式的支持：

```Manifest
[DriverRender]
XpsFormat = OpenXPS,XPS
```

该值指示通过 MSXPS 的首选项这两种格式的支持：

```Manifest
[DriverRender]
XpsFormat = XPS,OpenXPS
```

此决策基于功能旨在提供驱动程序和驱动程序开发人员确定其 V4 打印驱动程序的首选的格式。 例如，可以开发打印驱动程序为高保真图像提供 JPEG xr 增强支持。

打印系统做出各种决策基于在清单中的 DriverRender 信息。 下面是这些决策的一些示例：

-   基于 GDI 的打印作业发送到 v4 驱动程序

    Microsoft XPS 文档转换器 (MXDC) 采用 GDI 打印作业输入，并将作业转换为 XPS 假脱机文件。 该后台打印文件的格式将匹配表示清单的 DriverRender 部分中的首选的 XPS 格式。

-   XPS 打印 API 格式转换

    XPS 打印 API 将查询目标驱动程序支持的 XPS 格式。 如果该驱动程序支持这两种格式，XPS 打印 API 将 XPS 打印作业后台处理程序 AS 提交到通过传递应用程序。 将不执行任何转换。

    如果目标驱动程序仅支持一个或其他格式，该作业将转换为正确的格式之前后台处理。

    如果在清单中不提供任何 XpsFormat，则行为将仅默认为 MSXPS。 OpenXPS 输入将转换为 MSXPS。 此行为的驱动程序提供最强的向后兼容性。

-   XPS 文件直接发送到后台处理程序

    默认情况下，MSXPS 是直接发送到后台处理程序的 XPS 文件。 不支持提交 OpenXPS 将定向到后台处理程序。 但是，在 4.5 + 之前的.NET 序列化其自身 MSXPS，将作业提交直接到后台处理程序。 XPS 打印 API (xpsprint.dll) 在引入之前实现了此行为。

    若要为这些.NET 应用程序提供向后兼容性，打印筛选器管道管理器将检查后台打印文件以确定它是否接收到后台处理程序直接。 如果是这样，它将假定为 MSXPS。 打印筛选器管道管理器将在该点查询驱动程序的 XPS 格式。 如果该驱动程序支持 MSXPS，将不执行任何转换。 如果该驱动程序仅支持 OpenXPS，打印筛选器管道管理器将执行该文件的转换。 此时作业中的转换是性能成本高;但是，它可确保传统.NET 应用程序将能够打印到新的 v4 OpenXPS 驱动程序。

**驱动程序清单：存部分**。 V4 打印驱动程序清单的存部分提供了用于扩展**文件保存**对话框由 PORTPROMPT： 端口。 (PORTPROMPT： 应使用替代文件： 在 Windows 8.1，因为 PORTPROMPT： 将允许用户访问他们有权访问的即使在低权限模式下运行应用程序的所有文件位置。)存节中的项与相关联 DriverRender 节中的项的索引。

示例：

```Manifest
[FileSave]
xps=0
oxps=0

[DriverRender]
XpsFormat=XPS,OpenXPS
```

这将确保当用户将打印作业发送到此驱动程序，并且该端口设置为 PORTPROMPT:，则**文件保存**对话框将显示 XPS 和 OpenXPS 作为文件在对话框中，键入选项，并为文件分别应用.xps 或.oxps扩展插件。

有关清单的文件将保存部分其他选项的其他信息，请参阅[V4 驱动程序清单](v4-driver-manifest.md)。

## <a name="related-topics"></a>相关主题

[OpenXPS 打印的应用程序支持](https://docs.microsoft.com/windows/desktop/printdocs/app-support-for-openxps-printing)  

[Open XML 纸张规范](http://www.ecma-international.org/publications/standards/Ecma-388.htm) 

[V4 驱动程序清单](v4-driver-manifest.md)  
