---
title: 公共符号和专用符号
description: 公共符号和专用符号
ms.assetid: 83979008-f9ea-4976-8acd-d7efb82947cd
keywords:
- BinPlace WDK，公共符号
- BinPlace WDK，私有符号
- 符号文件 WDK BinPlace
- 私有符号 WDK BinPlace
- 公共符号 WDK BinPlace
- 减少符号文件中的符号
- 完整的符号文件必须 WDK BinPlace
- 去除 WDK BinPlace 的符号文件
- SymChk 工具 WDK BinPlace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652745217717313fe04268a494550ff37211f0e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358268"
---
# <a name="public-symbols-and-private-symbols"></a>公共符号和专用符号


## <span id="ddk_public_symbols_and_private_symbols_tools"></span><span id="DDK_PUBLIC_SYMBOLS_AND_PRIVATE_SYMBOLS_TOOLS"></span>


驱动程序或其他程序生成时，该程序的符号通常存储在*符号文件*，尽管某些较旧的编译器在可执行文件中存储某些符号。 在调试程序分析一个程序时，它需要访问该程序的符号。

通常情况下，符号文件可以包括任何或所有以下符号：

-   姓名和地址的所有函数

-   所有数据类型、 结构和类定义

-   名称、 数据类型和全局变量的地址

-   名称、 数据类型、 地址和本地变量的作用域

-   对应于每个二进制指令的源代码中的行号

某些程序开发人员可能会感到不安与客户共享所有此类信息。 BinPlace 可用来减少的符号文件中的符号。

即使最基本的调试，需要一些基本的符号，如函数名称和全局变量。 这些被称为*公共符号*。 如数据结构名称的符号，只有一个对象文件、 本地变量和行号信息中可见的全局变量并不总是必需进行调试，尽管它们是有用的更深入的调试会话。 这些被称为*私有符号*。

包含专用和公共符号的符号文件称为*完整符号文件*。 包含单独的公共符号的符号文件称为*符号文件中去除*。

BinPlace 可以创建去除的符号文件。 这是通过创建新的符号文件包含仅公共符号;私有符号是已删除 （"去除"）。 当使用最常用的 BinPlace 选项 (--x-s n)，去除的符号文件放置在后列出的目录 **-s**开关，并且完整的符号文件位于后列出在目录中 **-n**切换。

当 BinPlace 去除的符号文件时，去除和完整版本的文件有完全相同的签名和其他标识信息。 这可以使用任一版本进行调试。

**请注意**   BinPlace 会去除私有符号的符号文件超出在符号文件是与可执行文件相同的目录中并且你指定的名称*可执行文件*文件 (连同相应的选项） 在 BinPlace 命令行上。 不应指定符号文件本身-执行此操作的名称将导致 BinPlace 移动文件，而无需更改它。

 

如果您需要确定是否符号文件包含私有符号，可以使用[SymChk](https://docs.microsoft.com/windows-hardware/drivers/debugger/symchk)工具。 SymChk 是有关 Windows 调试工具软件包的一部分。 请参阅 SymChk 并[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)有关详细信息。

如果您要提交到您的驱动程序[Windows 硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)，可以提交去除的符号文件，如果不想与 Microsoft 共享你的私有符号。 已去除通过 BinPlace 的符号文件不会公开您的驱动程序的体系结构，通常会被视为机密的任何部分。 有关详细信息，请参阅[Windows 硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)。

 

 





