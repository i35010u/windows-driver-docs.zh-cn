---
title: 调试器数据模型 - 基本块对象
description: 基本块是代码的区域 （通常） 一个入口点和一个退出点。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c121f4969b21474dc301d6488dabaf166691f1cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567375"
---
# <a name="basic-block-objects"></a>基本块对象 
## <a name="summary"></a>总结
基本块是代码的区域 （通常） 一个入口点和一个退出点。 [拆装器](dbgmodel-object-disassembler.md)的 DisassembleBlocks 和 DisassembleFunction 方法都返回基本块的集合。 DisassembleBlocks 方法执行基本块的简单分析，并可能会导致多个入口点的块。 DisassembleFunction 将执行在单个条目和单个出口的基本块中生成的函数的完整流分析。
## <a name="object-properties"></a>对象属性
|“属性”|描述|
|--- |--- |
|StartAddress|基本块的起始地址。|
|EndAddress|基本块的结束地址。 块定义的半开集 [*StartAddress*， *EndAddress*)。|
|说明|一个[集合](dbgmodel-namespace-collections.md)的[指令](dbgmodel-object-instruction.md)基本块中的对象。|
|InboundControlFlows|此属性才是完整的流分析的结果基本块上存在 (例如：*DisassembleFunction*)。 它是[集合](dbgmodel-namespace-collections.md)的[控制流](dbgmodel-object-control-flow.md)对象描述其他块具有入站控制流到此链接。|
|OutboundControlFlows|此属性才是完整的流分析的结果基本块上存在 (例如：*DisassembleFunction*)。 它是[集合](dbgmodel-namespace-collections.md)的[控制流](dbgmodel-object-control-flow.md)对象描述出站控制流中此块对其他块在函数中的链接。|