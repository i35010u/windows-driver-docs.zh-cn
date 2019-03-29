---
title: 编写 INF 文件
description: 编写 INF 文件
ms.assetid: 0A31484C-3A61-4a6d-B500-E5C69E2130F9
keywords:
- INF 文件 WDK 设备安装编写
- 写入 WDK 设备安装的 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 983ff61588d3c7ed2f98254ba771042109e28d1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561889"
---
# <a name="writing-inf-files"></a>编写 INF 文件


当你编写[INF 文件](inf-files.md)为你[驱动程序包](driver-packages.md)，应遵循以下准则：

-   INF 文件必须使用有效的结构和语法将驱动程序在包验证检查在安装过程的开始处。

    使用[INFVerif](../devtest/infverif.md)工具验证结构和语法的 INF 文件。

-   INF 文件必须包含有效 INF [ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)并[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)部分。 从 Windows Vista 开始，操作系统不会复制到驱动程序包[驱动程序存储区](driver-store.md)除非它们是存在并且正确填写。

-   此外，有时需要在设备安装过程中复制 INF 文件，以便 Windows 可以找到它们而不会重复显示用户提示。 例如，多功能设备的基本 INF 文件可能会复制设备的各个函数的 INF 文件，以便 Windows 可以找到这些 INF 文件，而不提示用户，每次它可以安装设备的功能之一。

    从 Windows XP 中，如果你想要暂存其他 INF 文件按的 INF 文件驱动的安装过程，请使用[ **INF CopyINF 指令**](inf-copyinf-directive.md)。

    **请注意**  不要使用[ **INF CopyFiles 指令**](inf-copyfiles-directive.md)为副本 INF 文件。

     

-   驱动程序包的组件必须永远不会直接复制或删除直接到系统的 INF 文件 *%SystemRoot%/Inf*目录。 这会导致驱动程序的数字签名，可以在失效，并且这会导致驱动程序不成功加载。

 

 





