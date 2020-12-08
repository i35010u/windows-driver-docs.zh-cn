---
title: 在 Visual Studio 中调试源代码
description: 此过程介绍了如何在 Visual Studio 中进行源代码调试。
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d553aef502804824bfc7193a63b6dc1cc7ff688
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802881"
---
# <a name="source-code-debugging-in-visual-studio"></a>在 Visual Studio 中调试源代码

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Microsoft Visual Studio，然后安装 Windows 驱动程序工具包 (WDK) 。 有关详细信息，请参阅 [Windows 驱动程序开发](../index.yml)。

若要使用源调试，您必须在生成二进制文件时，您的编译器或链接器 ( .pdb 文件) 创建符号文件。 这些符号文件显示调试器如何与源行相对应的二进制说明。 此外，调试器必须能够访问实际的源文件。 有关详细信息，请参阅 [源路径](source-path.md)。

当你中断到目标计算机时，或者当目标计算机上运行的代码命中断点时，如果 Visual Studio 可以找到源文件，则 Visual Studio 会显示源代码。 您可以通过从 "**调试**" 菜单中选择一个 **步骤** 命令来单步执行源代码。 还可以通过单击源窗口的左栏来设置断点。 以下屏幕截图显示了 Visual Studio 调试器中的源代码窗口。

![visual studio 调试器中源代码的屏幕截图](images/sourcecodedebuggingvs01.png)

 

