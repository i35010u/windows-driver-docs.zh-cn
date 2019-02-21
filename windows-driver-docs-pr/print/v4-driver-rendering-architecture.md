---
title: V4 打印机驱动程序呈现体系结构
description: V4 打印机驱动程序模型的呈现体系结构是 XPSDrv 体系结构相同。
ms.assetid: 132BB5D5-426C-4449-8562-B5E43E331858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41b41db70243585742df0b22e74622e306584a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521454"
---
# <a name="v4-printer-driver-rendering-architecture"></a>V4 打印机驱动程序呈现体系结构


V4 打印机驱动程序模型的呈现体系结构的 XPSDrv 体系结构、 相同，XPS 筛选器管道也遵循相同的 Windows，其中几个值得注意添加的内容的上一版本中使用的设计。

## <a name="rendering-architecture-diagram"></a>呈现体系结构关系图


下图显示了 v4 打印机驱动程序的呈现体系结构选项。

![呈现 v4 打印机驱动程序的体系结构选项](images/v4xpsdrvarch.png)

以下段落介绍 IHV 筛选器在上图中，角色，并且还提供指导原则开发功能在此呈现体系结构中运行。

## <a name="print-filter-pipeline-configuration-file"></a>打印筛选器管道配置文件


打印筛选器管道配置文件格式中保持不变。 建议的命名约定： vv&lt;PDL&gt;-pipelineconfig.xml，vv 所在制造商代码的占位符。 示例 fapcl6-pipelineconfig.xml。 所有打印筛选器管道配置文件必须结尾 –pipelineconfig.xml 才能与打印 XPS 的 Windows 桌面应用程序兼容。

## <a name="ihv-rendering-filter"></a>IHV 呈现筛选器


此筛选器完成到设备 PDL 输出从 XPS 呈现。 它可能会根据需要使用 XPS 光栅化服务或第三方 RIP。 以下是有关设计呈现筛选器的一些准则。

**建议的输入的类型：** IXpsDocumentProvider.
使用 IXpsDocumentProvider 接口是速度快于使用流接口，因为序列化步骤避免在呈现过程通过的点的数量。

**建议的输出类型：** IPrintWriteStream.
完成此筛选器后，设备 PDL 应作为输出流。

**建议的命名约定：** 使用 vv&lt;PDL&gt;.dll。
其中，vv 是制造商代码的占位符。 提供 Fabrikam PostScript 呈现器的示例： faps.dll。

能够使用作为 PDL XPS 的设备可能支持不呈现的任何筛选器的情况下。 但是，某些设备可能需要执行操作并不适用于 Microsoft 标准的 UI 的 Printticket。 在这些情况下，Microsoft 建议您应将转换为设备兼容 PrintTicket XPS 呈现筛选器中。 这可确保使用标准用户界面和设备的最佳兼容性。

## <a name="ihv-feature-filter"></a>IHV 功能筛选器


IHV 功能筛选器启用的功能，如每张多处理、 水印制作，或页重新排序。 使用功能筛选器是方便地将功能添加到驱动程序，而无需更改基础 PDL 呈现。 以下是有关设计此类功能筛选器的一些准则。

**建议的输入的类型：** IXpsDocumentProvider.

**建议的输出类型：** IXpsDocumentConsumer.

对于具有多个 IHV 功能筛选器的制造商，我们建议，这些筛选器实现到同一个 DLL 作为单独的逻辑筛选器。 这鼓励代码共享，并可能会降低整体工作集中在打印期间。

## <a name="color-management"></a>颜色管理


V4 打印驱动程序支持颜色管理。 驱动程序应包括[Windows 颜色系统](https://msdn.microsoft.com/library/windows/hardware/ff563783)(WCS) 兼容的颜色配置文件或国际色彩联合会 (ICC) 颜色配置文件。 V4 打印驱动程序还可以为特定于设备的颜色表中使用的驱动程序属性包。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序呈现](v4-driver-rendering.md)  
[Windows 颜色系统](https://msdn.microsoft.com/library/windows/hardware/ff563783)  



