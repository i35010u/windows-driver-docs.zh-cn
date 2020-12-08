---
title: GDL 预处理器条件指令
description: GDL 预处理器条件指令
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0ef9b066a3a5d48db63f3a4cbfa254e260e812e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835943"
---
# <a name="gdl-preprocessor-conditional-directives"></a>GDL 预处理器条件指令


GDL 预处理器条件指令定义条件构造。 每个条件构造都以 **\# Ifdef** 指令开头，并由 **\# Endif** 指令终止。 在 between 之间， **\# Elseifdef** 指令可能出现零次、一次或多次。 如果任何已使用) 和最后一个 **\# Endif** 指令，则可选的 **\# Else** 指令必须出现在最后一个 **\# Elseifdef** 指令之间 (。

其中每个指令都将中间数据分区 (非预处理器指令) 为条件部分;在预处理过程中，将保留每个部分用于分析或删除的下一个阶段，如下所述。 始终会保留未处理且不包含在任何条件构造中的数据。

条件节指令可以嵌套。 从 **\# Ifdef** 到结束 **\# Endif** 的整个条件构造必须完全驻留在封闭条件构造的一个部分中。

GDL 使用以下条件指令：

[\#Ifdef](-ifdef-conditional-preprocessor-directive.md)

[\#Elseifdef](-elseifdef-conditional-preprocessor-directive.md)

[\#其它](-else-conditional-preprocessor-directive.md)

[\#Endif](-endif-conditional-preprocessor-directive.md)

 

 




