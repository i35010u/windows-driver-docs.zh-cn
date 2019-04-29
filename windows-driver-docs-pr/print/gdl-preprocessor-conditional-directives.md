---
title: GDL 预处理器条件指令
description: GDL 预处理器条件指令
ms.assetid: 5eb4bcbf-3f5e-44cc-b4e5-716a15e43b15
keywords:
- 指令 WDK GDL，源文件预处理器指令
- 源文件 WDK GDL，预处理器指令
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 508e588296219506421258d73e1f10200cc8553f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380017"
---
# <a name="gdl-preprocessor-conditional-directives"></a>GDL 预处理器条件指令


GDL 预处理器条件指令定义条件构造。 每个条件构造开头 **\#Ifdef**指令和终止 **\#Endif**指令。 在中间 **\#Elseifdef**指令可能会出现零，有一个或多个时间。 可选 **\#Else**指令必须显示最后一个之间 **\#Elseifdef**指令 （如果有使用） 和最后一个 **\#Endif**指令。

这些指令的每个分区为条件节，则允许插入数据 （非预处理器指令）每个部分是保留的分析的下一阶段或预处理如下所述过程中删除。 这并不是处理和不包含任何条件构造中的数据始终保留。

可以嵌套的条件部分指令。 从整个条件构造 **\#Ifdef**结束语 **\#Endif**必须位于完全封闭的条件构造的一部分。

GDL 使用以下条件指令：

[\#Ifdef](-ifdef-conditional-preprocessor-directive.md)

[\#Elseifdef](-elseifdef-conditional-preprocessor-directive.md)

[\#Else](-else-conditional-preprocessor-directive.md)

[\#Endif](-endif-conditional-preprocessor-directive.md)

 

 




