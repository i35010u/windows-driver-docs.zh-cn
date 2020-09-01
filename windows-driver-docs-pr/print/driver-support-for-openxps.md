---
title: OpenXPS 的驱动程序支持
description: OpenXPS 是文档的开放 XML 纸张规范格式，并基于 Ecma International 标准规范。
ms.assetid: 9BC9787E-A54D-4A11-B256-57BE5D206404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f272cd4bcfac048496fe991c091ee6ced7de1ae7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217745"
---
# <a name="driver-support-for-openxps"></a>OpenXPS 的驱动程序支持


OpenXPS 是文档的开放 XML 纸张规范格式，并基于 Ecma International 标准规范。

有关此规范的最新信息，请参阅 [OPEN XML 纸张规范](https://www.ecma-international.org/publications/standards/Ecma-388.htm)。

Windows 8 为 OpenXPS 提供完全支持，并提供对现有 Microsoft XPS 格式的持续支持。 本主题重点介绍通过 v4 驱动程序模型对 OpenXPS 的支持。 有关与 Windows 应用程序开发人员相关的 OpenXPS 支持，请参阅 [应用程序支持 OpenXPS 打印](/windows/desktop/printdocs/app-support-for-openxps-printing)。

## <a name="supported-openxps-scenarios"></a>支持的 OpenXPS 方案


已开发 Windows 打印路径，以确保提交的 XPS 格式与受支持的目标打印驱动程序格式匹配，并将根据需要转换格式。 Windows 还提供了用于查询打印驱动程序的 Api，以便应用程序可以提供兼容的元素，并避免打印系统内的任何其他转换。

打印驱动程序可以使用其清单来指示它是支持 Microsoft XPS、Open XPS 还是同时支持这两种格式。 可以在打印筛选器管道中向筛选器提供 Microsoft XPS 或 OpenXPS，使用现有流和对象模型 (OM) 接口–驱动程序无需使用新接口来支持 OpenXPS。 向筛选器提供的格式取决于驱动程序支持的格式或应用程序提供的格式。

Microsoft XPS 文档编写器 (MXDW) 已更新，以允许 MXDW 从任何 Windows 桌面应用程序输出 Microsoft XPS 或 OpenXPS。 同样，Windows 8 中的 Microsoft XPS 查看器和读者应用可以打开这两种 XPS 格式。 如果需要，用户可以从 XPS 查看器打印到 MXDW，以便转换格式。

## <a name="unsupported-openxps-scenarios"></a>不受支持的 OpenXPS 方案


某些旧功能可能不受支持，或在与 OpenXPS 一起使用时提供降级体验。

*不受支持*：不支持将 OpenXPS 文件直接发送到后台处理程序 (绕过 XPS 打印 API) 是不受支持的方案。 这样做会产生以下功能问题：

-   直接发送到后台处理程序的 XPS 假脱机文件将被视为 MSXPS 并进行相应处理。
-   将 OpenXPS 文件直接发送到后台处理程序的结果是未定义的，并且可能会导致打印作业失败。

**注意**   没有为此方案提供支持的计划。

 

*不建议*：不建议将 OpenXPS 流从应用程序直接发送到 XPS 打印 API。 例如，不要将 OpenXPS 流直接发送到 StartXPSPrintJob 方法。 如果执行此操作，则从一种形式的 XPS 转换为另一种流的结果可能会非常昂贵，从而降低性能。

相反，应使用 IPrintDocumentPackageTarget 将打印作业作为 XPS OM 提交，以避免性能下降。

*不建议*：将 XPS 假脱机文件直接发送到后台处理程序。 如果这样做，打印系统将找不到打印路径 Api 添加的所需元数据，假设格式为 MSXPS，并将尝试将其转换为 OpenXPS。 如果直接发送到后台处理程序的假脱机文件是 OpenXPS 格式的文件，则打印筛选器管道将其 "转换" 为 OpenXPS 时的尝试将会出现未定义的结果。 如果发送到后台处理程序的文件是 MSXPS 格式的文件，并且该驱动程序是仅限 OpenXPS 的驱动程序，则打印筛选器管道到 OpenXPS 的转换将会成功。 但这种延迟阶段转换将导致打印系统性能出现严重损失。

## <a name="impact-on-app-developers"></a>对应用程序开发人员的影响


有关适用于 Windows 8 对 OpenXPS 的支持的影响的信息，请参阅 [OpenXPS 打印的应用支持](/windows/desktop/printdocs/app-support-for-openxps-printing)。

## <a name="impact-on-driver-developers"></a>对驱动程序开发人员的影响


下面是在 v4 打印驱动程序中启用 OpenXPS 的基本步骤：

-   驱动程序清单：将 "OpenXPS" 添加到驱动程序呈现部分。
-   驱动程序清单：将 ".oxps" 添加到 FileSave 节（如果适用）。
-   筛选器管道：更新打印筛选器以处理 OpenXPS 元素。

对于给定的流，以及使用适当的对象接口，客户端可以使用 OpenXPS 格式将数据传输到打印筛选器管道中的筛选器。 若要传输数据流，客户端将使用 IID \_ IPrintReadStream 和 iid \_ IPrintWriteStream 接口。 若要将数据传输到 OM 组件，客户端将使用 IID \_ IXpsDocumentProvider 和 iid \_ IXpsDocumentConsumer 接口。 对于声明支持 OpenXPS 的驱动程序，将必须确保当从管道管理器收到此格式时，提供的打印筛选器可以正确地处理 OpenXPS 格式。

**驱动程序清单： DriverRender 部分**。 在驱动程序安装过程中，安装过程将检查清单的 DriverRender 部分，以查看 XpsFormat 条目是否包含 OpenXPS。 XpsFormat 项可以包括 Microsoft XPS 的 XPS () 和 OpenXPS，以指示双重支持。 在 XpsFormat 项中列出这两种格式的顺序决定了驱动程序的首选格式。

下面是有关如何更新 DriverRender 部分的一些示例。

仅指示支持 OpenXPS：

```Manifest
[DriverRender]
XpsFormat = OpenXPS
```

仅指示支持 MSXPS：

```Manifest
[DriverRender]
XpsFormat = XPS
```

指示支持这两种格式，具有 OpenXPS 的首选项：

```Manifest
[DriverRender]
XpsFormat = OpenXPS,XPS
```

指示支持这两种格式，具有 MSXPS 的首选项：

```Manifest
[DriverRender]
XpsFormat = XPS,OpenXPS
```

驱动程序开发人员确定其 V4 打印驱动程序的首选格式，此决定基于驱动程序的设计目的。 例如，可以开发打印驱动程序来提供 JPEG XR 对高保真图像的支持。

打印系统根据清单中的 DriverRender 信息进行各种决策。 下面是这些决策的一些示例：

-   发送到 v4 驱动程序的基于 GDI 的打印作业

    Microsoft XPS 文档转换器 (MXDC) 采用 GDI 打印作业输入，并将作业转换为 XPS 假脱机文件。 该假脱机文件的格式将与清单的 DriverRender 部分中表示的首选 XPS 格式匹配。

-   XPS 打印 API 格式转换

    XPS 打印 API 将查询目标驱动程序支持的 XPS 格式。 如果驱动程序支持这两种格式，则 XPS 打印 API 会将 XPS 打印作业传递到应用程序提交的后台处理程序。 不会执行任何转换。

    如果目标驱动程序仅支持一种或其他格式，则该作业将在后台处理转换为正确的格式。

    如果清单中未提供 XpsFormat，则该行为将默认为 MSXPS。 OpenXPS 输入将转换为 MSXPS。 此行为为驱动程序提供了最强的后向兼容性。

-   直接发送到后台处理程序的 XPS 文件

    默认情况下，将 XPS 文件直接发送到后台处理程序，MSXPS。 不支持将 OpenXPS 直接提交到后台处理程序。 但是，在4.5 之前的 .NET 会序列化其自己的 MSXPS，并直接将作业提交到后台处理程序。 此行为在引入 XPS 打印 API 之前实现 ( # A0) 。

    为了提供这些 .NET 应用程序的向后兼容性，打印筛选器管道管理器将检查假脱机文件，以确定是否已收到直接到后台处理程序。 如果是，将假定它是 MSXPS。 此时，打印筛选器管道管理器将查询驱动程序的 XPS 格式。 如果驱动程序支持 MSXPS，则不会执行任何转换。 如果驱动程序只支持 OpenXPS，则打印筛选器管道管理器将执行该文件的转换。 此时，在该作业中的转换性能昂贵;但是，它可确保旧的 .NET 应用能够打印到新的 v4 OpenXPS 驱动程序。

**驱动程序清单： FileSave 部分**。 V4 打印驱动程序清单的 FileSave 部分为 PORTPROMPT： port 使用的 **文件保存** 对话框提供扩展。  (PORTPROMPT：应在 Windows 8.1 中使用，因为 PORTPROMPT：允许用户访问他们有权访问的所有文件位置，即使应用程序在低权限模式下运行也是如此。 ) FileSave 节中的条目按索引与 DriverRender 部分中的条目关联。

示例：

```Manifest
[FileSave]
xps=0
oxps=0

[DriverRender]
XpsFormat=XPS,OpenXPS
```

这将确保当用户将打印作业发送到此驱动程序，并且该端口设置为 PORTPROMPT：时，" **文件保存** " 对话框将在对话框中将 Xps 和 OpenXPS 显示为 "文件类型" 选项，并分别应用 .xps 或 .oxps 作为文件扩展名。

有关清单的 "文件保存" 部分的其他选项的其他信息，请参阅 [V4 驱动程序清单](v4-driver-manifest.md)。

## <a name="related-topics"></a>相关主题

[OpenXPS 打印的应用支持](/windows/desktop/printdocs/app-support-for-openxps-printing)  

[Open XML 纸张规范](https://www.ecma-international.org/publications/standards/Ecma-388.htm) 

[V4 驱动程序清单](v4-driver-manifest.md)