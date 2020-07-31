---
title: 调试器数据模型 - 指令对象
description: 指令对象描述单个计算机指令。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2726da94f4efceb077b517c3a16a737072f3af1
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402302"
---
# <a name="instruction-objects"></a>指令对象

## <a name="summary"></a>总结

指令对象描述单个计算机指令，并通过基于指令的反汇编或[基本块](dbgmodel-object-basic-block.md)对象内容的一部分返回。

## <a name="object-properties"></a>对象属性

|名称|描述|
|--- |--- |
|地址|计算机指令的地址。|
|属性|说明有关指令的详细信息的[指令特性](dbgmodel-object-instruction-attributes.md)对象。|
|CodeBytes|表示组成计算机指令的字节的字节数组。|
|Length|指令在内存中使用的字节数。|
|LiveVariables|[实时变量](dbgmodel-object-live-variable.md)对象的[集合](dbgmodel-namespace-collections.md)，这些对象描述编译器优化器为此特定位置的变量发出的数据。|
|个数|描述指令的操作数的[操作数](dbgmodel-object-operand.md)对象的[集合](dbgmodel-namespace-collections.md)。|
|SourceInformation|一个[源信息](dbgmodel-object-source-information.md)对象，该对象描述计算机指令和更高级别的源代码之间的关系。|
|SourceDataFlow|函数内的[指令](dbgmodel-object-instruction.md)对象的集合，该[集合](dbgmodel-namespace-collections.md)包含计算机指令的源操作数的数据流。 **此方法需要加载[CodeFlow 扩展](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)。**|
