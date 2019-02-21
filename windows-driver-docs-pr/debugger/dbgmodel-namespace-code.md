---
title: 调试器数据模型-代码 Namespace
description: 包含代码和 dissasembly 的属性。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 268c3439d37765fea71e1068f91e7e597464e101
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524596"
---
> [!IMPORTANT]
>  此接口处于活跃开发阶段，并将更改。
>
# <a name="the-code-namespace"></a>代码 Namespace

## <a name="summary"></a>摘要
代码命名空间包含代码和反汇编的属性。 这样，拆装器对象，可以反汇编给定地址或函数并提供有关程序集存在的详细的信息以及任何变量或源的信息，如果创建可获取。

## <a name="sample"></a>示例
有关如何的端到端示例此命名空间和对象和使用，请查看 GitHub-上的示例 https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow 

## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|描述|
|--- |--- |--- |--- |
|CreateDisassembler| [disassembler](dbgmodel-object-disassembler.md)|CreateDisassembler([architecture])|创建指定的体系结构的拆装器对象。 体系结构可能是一个"ARM"、"ARM64"、"X64"或"X86"。 如果未指定体系结构，则假定 X64。 |
|TraceDataFlow|[集合](dbgmodel-namespace-collections.md)的[说明](dbgmodel-object-instruction.md)|TraceDataFlow([address])|查找在指定的指令处*地址*（或如果未不指定任何地址的当前指令指针） 和所有其源操作数。 此方法将向后指导完成查找受影响的跟踪指令源操作数的任何指令的函数的控制流。 **此方法需要加载找到 CodeFlow 扩展[此处](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)。**|

## <a name="remarks"></a>备注
CreateDisassembler 默认为"X64"目前，在某些时候，此行为将改为提取在当前线程的指令指针的模块的体系结构。