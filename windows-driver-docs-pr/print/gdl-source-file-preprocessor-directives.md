---
title: GDL 源文件预处理器指令
description: GDL 源文件预处理器指令
ms.assetid: cc0f807f-5c06-4add-bed1-c15c8251dc98
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL
- 分析器 WDK GDL，指令
- Include 指令 WDK GDL
- 预编译的指令 WDK GDL
- Define 指令 WDK GDL
- 取消指令 WDK GDL
- Ifdef 指令 WDK GDL
- Elseifdef 指令 WDK GDL
- Else 指令 WDK GDL
- Endif 指令 WDK GDL
- SetPPPrefix 指令 WDK GDL
- UndefinePrefix 指令 WDK GDL
- EnablePPDirective 指令 WDK GDL
- DisablePPDirective 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba7be92d123a993a953bcf7fbb665d9dc5efdc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368893"
---
# <a name="gdl-source-file-preprocessor-directives"></a>GDL 源文件预处理器指令


GDL 分析器，例如原始 GPD 分析器，支持预处理器指令。 任何其他分析之前处理操作的预处理器指令。 在预处理阶段，仅预处理器指令被识别和所有非指令项将被视为黑盒数据。 在预处理的短语，所有预处理器指令会从输入流以便后续分析阶段不需要应对的预处理器语法。

预处理器指令的目的是使您能够创建 GDL 或 GPD 分析器的多个版本运行的单个 GDL 文件。 如果你有分析器只会在某些分析器版本的功能，可以使用 **\#Ifdef**语句和替换功能的等效项。

预处理器指令使用特定[GDL 预处理器语法](gdl-preprocessor-syntax.md)并[GDL 预处理器关键字](gdl-preprocessor-keywords.md)。

GDL 预处理器指令为 GPD 预处理器指令的扩展。 GDL 和 GPD 预处理器指令之间的差异的详细信息，请参阅[GDL 之间的差异和 GPD 预处理](differences-between-gdl-and-gpd-preprocessing.md)。

GDL 预处理器指令是只有一种 GDL 指令。 有关其他类型的 GDL 指令的详细信息，请参阅[GDL 指令](gdl-directives.md)。

以下列表是 GDL 预处理器关键字的摘要：

-   **\#包括**引用另一个 GDL 文件以包含当前 GDL 文件。

-   **\#定义**并 **\#未定义**管理预处理器条件指令使用的符号的列表。

-   **\#预编译**创建表示 GDL 源文件可以动态链接到 GDL 数据结构，它表示另一个 GDL 文件此文件中包含的独立数据结构。 此指令可用于消除频繁使用的文件的冗余副本。

-   **\#Ifdef**，  **\#Elseifdef**，  **\#Else**，并且 **\#Endif**有条件地禁用 GDL 中的部分源文件。 这些指令可以引用由预处理器条件指令定义的符号或符号定义的不同版本的 GDL 分析器。

-   **\#SetPPPrefix**，  **\#UndefinePrefix**，  **\#EnablePPDirective**，并且 **\#DisablePPDirective**修改指令的处理。

本部分包括：

[GDL 预处理器语法](gdl-preprocessor-syntax.md)

[GDL 预处理器关键字](gdl-preprocessor-keywords.md)

[GDL 和 GPD 预处理之间的差异](differences-between-gdl-and-gpd-preprocessing.md)

[GDL 预处理器的指导原则](gdl-preprocessor-guidelines.md)

 

 




