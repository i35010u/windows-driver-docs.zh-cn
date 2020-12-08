---
title: GDL 源文件预处理器指令
description: GDL 源文件预处理器指令
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL
- 分析器 WDK GDL，指令
- Include 指令 WDK GDL
- 预编译的指令 WDK GDL
- 定义指令 WDK GDL
- 取消定义指令 WDK GDL
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
ms.openlocfilehash: 8b9730d448465d3c79842cbcde5ac05a33e19a87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796945"
---
# <a name="gdl-source-file-preprocessor-directives"></a>GDL 源文件预处理器指令


GDL 分析器（如原始 GPD 分析器）支持预处理器指令。 预处理器指令在进行任何其他分析之前处理。 在预处理阶段，只会识别预处理器指令，并将所有非指令条目视为黑白数据。 在预处理短语期间，将从输入流中删除所有预处理器指令，以便随后的分析阶段不需要与预处理器语法进行争用。

预处理器指令的用途是使你能够创建在多个版本的 GDL 或 GPD 分析器上运行的单个 GDL 文件。 如果你的分析器功能仅在某些分析器版本上出现，则可以使用 **\# Ifdef** 语句，并将该功能替换为等效项。

预处理器指令使用特定的 [GDL 预处理器语法](gdl-preprocessor-syntax.md) 和 [GDL 预处理器关键字](gdl-preprocessor-keywords.md)。

GDL 预处理器指令是 GPD 预处理器指令的扩展。 有关 GDL 和 GPD 预处理器指令之间的差异的详细信息，请参阅 [GDL 和 GPD 预处理之间的差异](differences-between-gdl-and-gpd-preprocessing.md)。

GDL 预处理器指令只是一种 GDL 指令。 有关其他类型的 GDL 指令的详细信息，请参阅 [GDL 指令](gdl-directives.md)。

以下列表汇总了 GDL 预处理器关键字：

-   **\# Include** 引用包含在当前 GDL 文件中的另一个 GDL 文件。

-   **\# 定义** 和 **\# 取消** 定义预处理器条件指令使用的符号列表。

-   **\# 预编译** 会创建一个独立的数据结构，该结构表示此文件中包含的 GDL 源文件，该文件可以动态链接到代表另一个 GDL 文件的 GDL 数据结构。 您可以使用此指令消除经常使用的文件的冗余副本。

-   **\# Ifdef**、 **\# Elseifdef**、 **\# Else** 和 **\# Endif** 有条件地禁用了 GDL 源文件中的部分。 这些指令可以引用由预处理器条件指令或由不同版本的 GDL 分析器定义的符号。

-   **\# SetPPPrefix**、 **\# UndefinePrefix**、 **\# EnablePPDirective** 和 **\# DisablePPDirective** 修改指令处理。

本节包括：

[GDL 预处理器语法](gdl-preprocessor-syntax.md)

[GDL 预处理器关键字](gdl-preprocessor-keywords.md)

[GDL 与 GPD 预处理之间的差异](differences-between-gdl-and-gpd-preprocessing.md)

[GDL 预处理器指导原则](gdl-preprocessor-guidelines.md)

 

 




