---
title: 已检验版本和免费版本的差异
description: 基于 NT 的操作系统有两个不同的版本可用（零售）和选中（调试）。 还有第三个选项（称为部分检查的生成），它将两个元素组合在一起。
ms.assetid: 43aebfdb-2605-485c-a3a4-93e03b33aeca
keywords:
- checked build WDK，与免费版本
- 免费生成 WDK
- 零售版本 WDK
ms.date: 09/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7fdc411da56c9aa4f14e31de833a0bda1cec4ae3
ms.sourcegitcommit: f018b0ab82aae3e3779128d3c4420222ddc0f4ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71329601"
---
# <a name="checked-and-free-build-differences"></a>已检验版本和免费版本的差异

提供了两个不同的基于 NT 的操作系统版本：免费（零售）和检查（调试）。 还有第三个选项（*称为部分检查的生成*），它将两个元素组合在一起。

- [已检查和免费生成之间的差异](#differences-between-the-checked-and-free-builds)
- [在何处可以找到 Windows 的已检查版本](#where-to-find-a-checked-build-of-windows)
- [何时使用选中的生成或部分选中的生成](#when-to-use-the-checked-build-or-partial-checked-build)

## <a name="differences-between-the-checked-and-free-builds"></a>已检查和免费生成之间的差异

本节列出了生成选项之间的一些差异。

**免费生成（或零售版本）**  
在生产环境中使用 Microsoft Windows 的免费版本。 操作系统的免费版本是用完全编译器优化生成的。 当免费版本发现可纠正的问题时，它将继续运行。

包含操作系统的免费版本的分发媒体没有任何特殊标签，换言之，包含免费版本的 CD 或下载标记有 Windows 版本名称，没有任何版本的版本的任何引用。

**检查的生成（或调试版本）**  
Microsoft Windows 的检查内部版本可让你更轻松地识别和诊断操作系统级问题。

检查的生成与免费生成在以下方面有所不同：

- 许多编译器优化（如堆栈帧消除）在检查的生成中被禁用。 这样可以更轻松地了解拆装的机器说明，因此更容易跟踪系统软件问题的原因。

- 选中的生成在操作系统代码和系统提供的驱动程序中启用大量的调试检查。 这可帮助选中的生成在发生内部不一致和问题时立即识别它们。

**部分检查的生成（或部分调试内部版本）**  
Microsoft Windows 的部分检查的内部版本与完整检查的版本类似。 主要区别在于部分检查的生成仅包括已检查的操作系统映像（内核）和检查的硬件抽象层（HAL）。 Windows 组件的其余部分来自 Windows 的免费（零售）版本。

部分检查的生成与免费和完整检查的生成的不同之处在于：

- 与完整检查的版本一样，禁用了许多编译器优化（如堆栈帧消除）。 这样就可以更轻松地了解拆装的机器说明，因此更容易跟踪问题的原因。

- 部分检查的生成在操作系统代码和 HAL 中启用了许多调试检查。 但是，系统提供的驱动程序来自免费（零售）版本，因此除非你显式安装了系统提供的驱动程序的已检查版本，否则你不会获得完全检查的版本的其他优点来识别和调试问题。

- 部分检查的生成要求您首先安装 Windows 的完整免费（零售）版本。 使用启动选项，你可以将计算机配置为在启动时加载已检查或可用的组件。 然后，你可以使用一台计算机通过 Windows 的已检查和免费版本来测试驱动程序。

## <a name="where-to-find-a-checked-build-of-windows"></a>在何处可以找到 Windows 的已检查版本

包含选中版本的下载和分发媒体清楚地标记为 "调试/选中生成"。 所选的生成下载包含操作系统的已检查版本，以及所选版本的 Hal、驱动程序、文件系统，甚至许多用户模式组件。 有关获取选中并部分检查的生成的信息，请参阅[安装检查的生成](installing-the-checked-build.md)。 为方便起见，在 Windows 驱动程序工具包（从适用于 Windows Vista 的 WDK）中提供了所选版本的内核和 HAL。

## <a name="when-to-use-the-checked-build-or-partial-checked-build"></a>何时使用选中的生成或部分选中的生成

需要测试驱动程序时，应始终在开发过程中的某个时间点使用检查的生成。 检查的生成会在驱动程序与操作系统交互的方式中公开问题。 如果未测试您的驱动程序是否能够在检查的内部版本中运行，则不会将测试视为已完成。

由于检查的生成包含的优化和调试检查比免费生成更少，因此检查后的生成的大小和运行时间比免费版本慢。 因此，免费生成在生产环境中使用，除非需要使用 checked 生成来确定严重的问题。

作为完整检查版本的替代方法，你可以将计算机配置为使用部分检查的生成。 这为你提供了用于调试的检查生成的优点，以及免费生成的更好性能。 有关将计算机配置为部分检查的版本的信息，请参阅[仅安装已检查的操作系统和 HAL （适用于 Windows Vista 及更高版本）](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)。

若要在使用部分检查的生成时对驱动程序进行更全面的测试，还应考虑安装所选的相关系统驱动程序的版本。 例如，如果要开发较低的磁盘筛选器驱动程序，应考虑从完整的已检查版本提取并安装磁盘 .sys 和 Storport 的已检查内部版本。

若要验证是否正在运行检查生成，请按照步骤 4-[仅安装已检查操作系统和 HAL （适用于 Windows Vista 和更高版本）](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)中的**步骤 4-重新启动计算机**中的说明操作。