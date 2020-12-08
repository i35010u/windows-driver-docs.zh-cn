---
title: 编写 INF 文件
description: 编写 INF 文件
keywords:
- INF 文件 WDK 设备安装，写入
- 编写 INF 文件 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b11a0aaab377739c13f5fa483a73315a94acc68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817719"
---
# <a name="writing-inf-files"></a>编写 INF 文件


为[驱动程序包](driver-packages.md)编写[INF 文件](overview-of-inf-files.md)时，应遵循以下准则：

-   INF 文件在安装过程开始时，必须使用有效的结构和语法来传递驱动程序包验证检查。

    使用 [INFVerif](../devtest/infverif.md) 工具验证 INF 文件的结构和语法。

-   INF 文件必须包含有效的 INF [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) 和 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 部分。 从 Windows Vista 开始，操作系统不会将驱动程序包复制到 [驱动程序存储区](driver-store.md) 中，除非这些部分存在并正确填充。

-   有时需要在设备安装过程中复制 INF 文件，以便 Windows 可以在不重复显示用户提示的情况下找到它们。 例如，多功能设备的基本 INF 文件可能会复制设备的各个功能的 INF 文件，以便 Windows 无需在每次安装设备的功能时提示用户，就能找到这些 INF 文件。

    从 Windows XP 开始，如果想要在由 INF 文件驱动的安装过程中暂存其他 INF 文件，请使用 [**Inf CopyINF 指令**](inf-copyinf-directive.md)。

    **注意**  不要使用 [**Inf CopyFiles 指令**](inf-copyfiles-directive.md) 复制 inf 文件。

     

-   驱动程序包的组件决不能直接将 INF 文件直接复制或删除到系统的 *% SystemRoot%/Inf* 目录中。 这将导致驱动程序的数字签名失效，这将导致驱动程序无法成功加载。

 

 





