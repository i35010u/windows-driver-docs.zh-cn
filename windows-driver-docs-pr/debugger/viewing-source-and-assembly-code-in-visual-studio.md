---
title: 在 Visual Studio 中调试源代码
description: 该过程介绍了 Visual Studio 中的源代码调试。
ms.assetid: C2E5BAA8-913A-4B0E-8ADF-E2758CCFEC84
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 637aaa7dcc91cdc3ed7bbf0a0d83c97170767913
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325929"
---
# <a name="source-code-debugging-in-visual-studio"></a>在 Visual Studio 中调试源代码

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>

本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Microsoft Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows 驱动程序开发](https://msdn.microsoft.com/library/windows/hardware/ff557573)。

若要使用源代码调试，必须具有编译器或链接器创建符号文件 （.pdb 文件） 时生成二进制文件。 这些符号文件显示在调试器的二进制说明如何与源行相对应。 此外，调试器必须能够访问的实际源文件。 有关详细信息，请参阅[源路径](source-path.md)。

中断到目标计算机时或当目标计算机上运行的代码达到断点时，Visual Studio 将显示源代码，如果它能找到的源文件。 可以通过选择之一逐句通过源代码**步骤**命令从**调试**菜单。 此外可以通过单击源窗口的左列中设置断点。 下面的屏幕截图显示了 Visual Studio 调试器中的源代码窗口中。

![在 visual studio 调试器中的源代码的屏幕截图](images/sourcecodedebuggingvs01.png)

 

 





