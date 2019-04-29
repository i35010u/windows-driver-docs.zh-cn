---
title: 打印机 INF 文件中的修饰
description: 打印机 INF 文件中的修饰
ms.assetid: 86ddca11-e2a9-44b8-8c42-313116fc580e
keywords:
- INF 文件 WDK 打印，修饰
- 其他驱动程序 WDK 打印机
- 修饰的 INF WDK
- INF Models 节
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3340d38b2982220d757a2c593a620e74fefd32a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384958"
---
# <a name="decorations-in-printer-inf-files"></a>打印机 INF 文件中的修饰


打印机设备安装程序类是唯一的而设备类的功能，以便针对不同处理器体系结构编写驱动程序。 例如，x86 打印机驱动程序 (一个包含的 x86 二进制文件) 可以添加到 x64 计算机。 在此示例中的驱动程序永远不会在 x64 执行的 x86 计算机-它提供了指向并打印支持针对 x86 客户端。 添加针对不同的体系结构的客户端调用的支持指向并打印的打印机驱动程序*其他驱动程序*。 指向并打印有关的信息，请参阅[简介指向并打印](introduction-to-point-and-print.md)。

因为需要加载其他驱动程序适用于不同的处理器体系结构 (即，x86、 x64 和 Itanium 体系结构)，Microsoft Windows Server 2003 SP1 和更高版本中的打印机类安装程序和 Windows XP 的 64 位版本和接下来，使用中的修饰[ **INF 模型部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)来标识计算机体系结构的驱动程序目标。

### <a name="inf-file-decorations-and-windows-versions"></a>INF 文件修饰类型和 Windows 版本

Windows XP 中引入了打印机 INF 文件中的修饰。 在 Windows XP 和 Windows Server 2003 中，修饰是可选的。 如果指定了修饰 INF 模型部分中的，它们应匹配当前处理器体系结构。

从 Windows Server 2003 SP1 和 Windows XP 的 64 位版本开始，将不再适用于 x64 可选 INF 模型部分中的修饰驱动程序;这些驱动程序必须使用修饰的 INF 模型部分来指示其目标计算机。

[如何将使用的打印机驱动程序的 INF 文件中的修饰](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

 

 




