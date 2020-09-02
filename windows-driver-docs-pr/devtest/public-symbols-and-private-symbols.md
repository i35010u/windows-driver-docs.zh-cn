---
title: 公共符号和专用符号
description: 公共符号和专用符号
ms.assetid: 83979008-f9ea-4976-8acd-d7efb82947cd
keywords:
- BinPlace WDK，公共符号
- BinPlace WDK，专用符号
- 符号文件 WDK BinPlace
- 私有符号 WDK BinPlace
- 公共符号 WDK BinPlace
- 减小符号文件中的符号
- 完全符号文件 WDK BinPlace
- 去除符号文件 WDK BinPlace
- SymChk 工具 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f351d1a29f3e6072fafc51a9ebfd96ef7ef25539
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382977"
---
# <a name="public-symbols-and-private-symbols"></a>公共符号和专用符号


## <span id="ddk_public_symbols_and_private_symbols_tools"></span><span id="DDK_PUBLIC_SYMBOLS_AND_PRIVATE_SYMBOLS_TOOLS"></span>


构建驱动程序或其他程序时，该程序的符号通常存储在 *符号文件*中，不过一些较旧的编译器会将某些符号存储在可执行文件中。 当调试器分析程序时，它需要访问程序的符号。

通常，符号文件可以包含以下任何或所有符号：

-   所有函数的名称和地址

-   所有数据类型、结构和类定义

-   全局变量的名称、数据类型和地址

-   局部变量的名称、数据类型、地址和范围

-   源代码中对应于每个二进制指令的行号

某些程序开发人员可能会感到不安，与客户共享所有这些信息。 BinPlace 可用于减少符号文件中的符号量。

即使是最基本的调试，也需要一些基本符号，如函数名称和全局变量。 它们称为 *公共符号*。 尽管它们对于更深入的调试会话很有用，但这些符号（例如数据结构名称、只能在一个对象文件、局部变量和行号信息中看到的全局变量）不一定需要用于调试。 它们称为 *私有符号*。

包含私有和公共符号的符号文件称为 " *完整符号文件*"。 仅包含公共符号的符号文件称为 " *去除符号文件*"。

BinPlace 可以创建一个去除的符号文件。 它通过创建仅包含公共符号的新符号文件来实现此功能;删除私有符号 ( "去除") 。 如果使用最常见的 BinPlace 选项 (--x-n) ，则会将去除的符号文件放置在 **-s** 开关之后列出的目录中，并将完整的符号文件放在 **-n** 开关之后列出的目录中。

当 BinPlace 去除某个符号文件时，会为该文件的去除文件和完整版本提供相同的签名和其他标识信息。 这允许你使用任一版本进行调试。

**注意**   当符号文件与可执行文件位于同一目录中时，BinPlace 将从符号文件中去除私有符号，并指定*可执行*文件的名称以及在 BinPlace 命令行上) 相应选项 (。 不应指定符号文件本身的名称，这样做会导致 BinPlace 移动文件而不进行更改。

 

如果需要确定符号文件是否包含私有符号，可以使用 [SymChk](../debugger/symchk.md) 工具。 SymChk 是 Windows 包调试工具的一部分。 有关详细信息，请参阅 SymChk 和 [Windows 调试](../debugger/index.md) 。

如果要将驱动程序提交到 [Windows 硬件认证计划](/windows-hardware/test/hlk/user/windows-hardware-lab-kit-user-s-guide)，如果不想与 Microsoft 共享私有符号，可以提交去除的符号文件。 BinPlace 去除的符号文件不会公开您的驱动程序体系结构中通常会被视为机密的任何部分。 有关详细信息，请参阅 [Windows 硬件认证计划](/windows-hardware/test/hlk/user/windows-hardware-lab-kit-user-s-guide)。

 

