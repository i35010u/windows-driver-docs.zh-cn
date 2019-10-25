---
title: V4 打印机驱动程序渲染体系结构
description: V4 打印机驱动程序模型的呈现体系结构与 XPSDrv 体系结构相同。
ms.assetid: 132BB5D5-426C-4449-8562-B5E43E331858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0097f44af4762f9c2f068e5040edd2b84d74acf9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843611"
---
# <a name="v4-printer-driver-rendering-architecture"></a>V4 打印机驱动程序渲染体系结构


V4 打印机驱动程序模型的呈现体系结构与 XPSDrv 体系结构相同，并且 XPS 筛选器管道还遵循在以前版本的 Windows 中使用的相同设计，但有一些值得注意的问题。

## <a name="rendering-architecture-diagram"></a>呈现体系结构关系图


下图显示了 v4 打印机驱动程序的呈现体系结构选项。

![v4 打印机驱动程序的呈现体系结构选项](images/v4xpsdrvarch.png)

以下各段说明了上图中 IHV 筛选器的角色，并提供了用于开发在此呈现体系结构中工作的功能的指南。

## <a name="print-filter-pipeline-configuration-file"></a>打印筛选器管道配置文件


打印筛选器管道配置文件的格式不相同。 建议的命名约定： vv&lt;PDL&gt;-pipelineconfig，其中 vv 是制造商代码的占位符。 示例 fapcl6-pipelineconfig。 所有打印筛选器管道配置文件都必须以– pipelineconfig 结尾，才能与打印 XPS 的 Windows 桌面应用程序兼容。

## <a name="ihv-rendering-filter"></a>IHV 呈现筛选器


此筛选器完成从 XPS 到设备 PDL 输出的呈现。 它可以根据需要使用 XPS 光栅化服务或第三方 RIP。 下面是一些用于设计呈现筛选器的准则。

**推荐的输入类型：** IXpsDocumentProvider.
使用 IXpsDocumentProvider 接口比使用流接口更快，因为在呈现过程中，可通过多个点避免序列化步骤。

**建议的输出类型：** IPrintWriteStream.
完成此筛选器后，设备 PDL 应作为流输出。

**建议的命名约定：** 使用 vv&lt;PDL&gt;.dll。
其中，vv 是制造商代码的占位符。 示例：用于 Fabrikam 提供的 PostScript 呈现器的 faps。

在没有任何呈现筛选器的情况下，可能会支持能够将 XPS 作为 PDL 使用的设备。 但是，某些设备可能需要 Printticket，它们无法与 Microsoft 标准 UI 一起使用。 在这些情况下，Microsoft 建议你应在 XPS 呈现筛选器中转换为与设备兼容的 PrintTicket。 这可确保与标准用户界面和设备的兼容性最佳。

## <a name="ihv-feature-filter"></a>IHV 功能筛选器


IHV 功能筛选器支持处理多个功能，例如，对多个功能进行预处理、水印或页面重新排序。 使用功能筛选器是向驱动程序添加功能的一种简便方法，无需更改基础 PDL 呈现。 下面是设计此类功能筛选器的一些准则。

**推荐的输入类型：** IXpsDocumentProvider.

**建议的输出类型：** IXpsDocumentConsumer.

对于具有多个 IHV 功能筛选器的制造商，我们建议将这些筛选器实现为与单独的逻辑筛选器相同的 DLL。 这鼓励代码共享，并可以在打印期间降低总体工作集。

## <a name="color-management"></a>颜色管理


V4 打印驱动程序支持颜色管理。 驱动程序应包括[Windows 颜色系统](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)（WCS）兼容颜色配置文件或国际颜色联合会（ICC）颜色配置文件。 V4 打印驱动程序还可以对特定于设备的颜色表使用驱动程序属性包。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序呈现](v4-driver-rendering.md)  
[Windows 颜色系统](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)  



