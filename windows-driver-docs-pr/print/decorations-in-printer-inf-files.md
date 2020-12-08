---
title: 打印机 INF 文件中的修饰
description: 打印机 INF 文件中的修饰
keywords:
- INF 文件 WDK 打印，装饰品
- 其他驱动程序 WDK 打印机
- 修饰 INF WDK
- INF Models 节
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e415a915564e5fe826128a71ef12fdb23ee0986c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797321"
---
# <a name="decorations-in-printer-inf-files"></a>打印机 INF 文件中的修饰


打印机设备安装程序类在设备类中是唯一的，因为它能够容纳为不同的处理器体系结构编写的驱动程序。 例如，x86 打印机驱动程序 (一个包含 x86 二进制文件的) 可添加到 x64 计算机。 在此示例中，x86 驱动程序从不在 x64 计算机上执行-它为 x86 客户端提供点和打印支持。 添加到支持点并打印给不同体系结构的客户端的打印机驱动程序称为 *附加驱动程序*。 有关点和打印的信息，请参阅 [指向和打印简介](introduction-to-point-and-print.md)。

由于需要为不同的处理器体系结构加载其他驱动程序 (也就是说，对于 x86、x64 和 Itanium 体系结构) ，Microsoft Windows Server 2003 SP1 及更高版本中的打印机类安装程序以及 Windows XP 及更高版本的64位版本使用 " [**INF 模型" 部分**](../install/inf-models-section.md) 中的修饰来确定驱动程序所针对的计算机的体系结构。

### <a name="inf-file-decorations-and-windows-versions"></a>INF 文件装饰和 Windows 版本

Windows XP 中引入了打印机 INF 文件中的修饰。 在 Windows XP 和 Windows Server 2003 中，修饰是可选的。 指定 INF 模型部分中的修饰时，它们应与当前处理器体系结构匹配。

从 Windows Server 2003 SP1 和 Windows XP 的64位版开始，"INF 模型" 部分中的修饰对于 x64 驱动程序不再是可选的;这些驱动程序必须使用修饰的 INF 模式部分来指示其目标计算机。

[如何使用打印机驱动程序 INF 文件中的修饰](how-to-use-decorations-in-inf-files-for-printer-drivers.md)

 

