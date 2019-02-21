---
title: Checked 和免费生成差异
description: 有两个非重复生成的基于 NT 的操作系统的可用免费 （零售） 并选中 （调试）。 还有一个名为部分已检验的版本，结合了两个元素的第三个选项。
ms.assetid: 43aebfdb-2605-485c-a3a4-93e03b33aeca
keywords:
- 检查内部版本号 WDK，与免费版本
- 免费生成 WDK
- 零售生成 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b23da3179e4241544f0dd3d12c5ec2066ccd55c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526084"
---
# <a name="checked-and-free-build-differences"></a>Checked 和免费生成差异


有两个不同内部提供的基于 NT 的操作系统： 释放 （零售） 并选中 （调试）。 还有第三个选项，*称为部分已检验的版本*，它将两个元素。

- [选中与免费之间的差异生成](#differences-between-the-checked-and-free-builds)
- [在哪里可以找到 Windows 已检验的版本](#where-to-find-a-checked-build-of-windows)
- [何时使用已检验的版本或部分已检验的版本](#when-to-use-the-checked-build-or-partial-checked-build)

## <a name="differences-between-the-checked-and-free-builds"></a>选中与免费之间的差异生成


本部分列出了一些生成选项之间的差异。

**免费生成 （或零售版本）**  
Microsoft Windows 的免费版本的生产环境中使用。 操作系统的免费版本生成了全面的编译器优化。 当免费生成就会发现可纠正问题时，它继续运行。

在分发媒体包含操作系统的免费版本不具有任何特殊标签-换而言之，CD 或下载，其中包含免费生成带有 Windows 版本名称，而不引用任何生成的类型。

**已检验的版本 （或调试版本）**  
Microsoft Windows 的已检验的版本可以识别和诊断运行系统级别问题更容易。

已检验的版本不同于免费版的以下方法：

- 已检验版本中禁用了 （例如堆栈帧消除） 的许多编译器优化。 这使得更易于理解已拆装的机器指令，并因此是更轻松地跟踪在系统软件问题的原因。

- 已检验的版本启用大量的调试检查中的操作系统代码和系统提供的驱动程序。 这有助于调试内部版本中，以确定内部不一致和问题，就立即发生。

**部分已检验的版本 （或部分的调试版本）**  
部分已检查生成的 Microsoft Windows 是类似于完整的调试内部版本。 主要区别在于部分已检验的版本包括唯一选中的操作系统映像 （内核） 和已检查的硬件抽象层 (HAL)。 组件来自的 Windows 的其余部分可用 （零售） 构建的 Windows。

部分已检验的版本不同于免费版和完整检查内部版本号如下：

-   完整的调试内部版本，如已禁用 （例如堆栈帧消除） 的许多编译器优化。 这使得更易于理解已拆装的机器指令，并因此是更轻松地跟踪问题的原因。

-   部分已检验的版本可以使用多个操作系统代码和 HAL 中的调试检查。 但是，系统提供驱动程序来自免费 （零售购买） 生成，因此除非你显式安装的系统提供的驱动程序付费版本，则无法获得完整的调试内部版本，以识别和调试问题的其他优势。

-   部分已检验的版本需要首先安装 Windows 完成免费 （零售购买） 生成。 使用启动选项，可以配置要在启动时加载是选中还是免费组件的计算机。 然后，可以使用一台计算机进行测试的选中和免费版本的 Windows 驱动程序。

## <a name="where-to-find-a-checked-build-of-windows"></a>在哪里可以找到 Windows 已检验的版本


下载和分发媒体包含已检验的版本具有明显的标签为"调试/已检验生成"。 已检验的版本下载包含的经检查的版本的操作系统，以及检查的版本的 Hal，驱动程序、 文件系统和多个用户模式组件。 有关获取选中和部分检查内部版本号的信息，请参阅[安装检查生成](installing-the-checked-build.md)。 为方便起见，Windows 驱动程序工具包 （WDK 为 Windows Vista 从开始） 的 /debug 目录中提供了对内核和 HAL 的付费版本。

## <a name="when-to-use-the-checked-build-or-partial-checked-build"></a>何时使用已检验的版本或部分已检验的版本


您应始终使用已检验的版本中的某个时刻在开发过程中需要进行测试驱动程序时。 已检验的版本可以公开该驱动程序与操作系统交互的方式中的问题。 没有测试可以被视为完成而无需测试您的驱动程序是能够在不会出现问题的已检验版本中运行。

由于已检验的版本包含较少的优化和于免费版本的更多调试检查，因此已检验的版本是更大的大小和速度较慢于免费版本运行。 结果是，会在生产环境中使用免费生成，除非它被使用已检验的版本以确定严重问题所需多。

作为完整的调试内部版本的替代方法，可以配置为使用部分已检验的版本的计算机。 这使您的内部版本以进行调试，优点以及的免费生成更好的性能。 有关部分已检验版本将计算机配置的信息，请参阅[安装只需检查操作系统和 HAL （适用于 Windows Vista 和更高版本）](installing-just-the-checked-operating-system-and-hal--for-windows-vist.md)。

有关更完整的测试您的驱动程序使用部分已检验的版本时，您还考虑安装相关的系统提供驱动程序的付费版本。 例如，如果你正在开发的较低的磁盘筛选器驱动程序，则应考虑中提取并从完整的调试内部版本安装的 Disk.sys 和 Storport.sys 内部的版本。

 

 





