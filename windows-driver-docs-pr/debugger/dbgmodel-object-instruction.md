---
title: 调试器数据模型-指令对象
description: 指令对象描述单个机器指令。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4513cbdb5235341d962f212ab46b9267decfb75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542641"
---
# <a name="instruction-objects"></a>指令的对象 
## <a name="summary"></a>摘要
指令的对象描述单个机器指令，并通过任一基于指令反汇编或作为内容的一部分返回[基本块](dbgmodel-object-basic-block.md)对象。 
## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|地址|计算机指令的地址。|
|属性|[指令属性](dbgmodel-object-instruction-attributes.md)对象描述有关指令的详细信息。|
|CodeBytes|表示构成该机器指令的字节的字节数组。|
|长度|在内存中的指令所采用的字节数。|
|LiveVariables|一个[集合](dbgmodel-namespace-collections.md)的[实时变量](dbgmodel-object-live-variable.md)描述编译器优化器发出有关此特定位置的变量的数据的对象。|
|操作数|一个[集合](dbgmodel-namespace-collections.md)的[操作数](dbgmodel-object-operand.md)描述指令的操作数对象。|
|SourceInformation|一个[源信息](dbgmodel-object-source-information.md)对象描述的机器指令和更高级别源代码之间的关系。|
|SourceDataFlow|一个[集合](dbgmodel-namespace-collections.md)的[指令](dbgmodel-object-instruction.md)包含数据流源机器指令的操作数，它们在函数内的对象。 **此方法需要加载找到 CodeFlow 扩展[此处](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)。**|