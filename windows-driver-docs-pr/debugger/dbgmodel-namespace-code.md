---
title: 调试器数据模型 - 代码命名空间
description: 包含代码和 dissasembly 的特性。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 121a93cab47d78df8ce611f57717de5a77d1b47c
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402236"
---
# <a name="the-code-namespace"></a>代码命名空间

> [!IMPORTANT]
> 此接口处于积极开发阶段，会发生更改。
>

## <a name="summary"></a>总结

代码命名空间包含代码和反汇编的特性。 它允许创建拆装器对象，这些对象可以反汇编给定的地址或函数并提供有关程序集的详细信息以及任何变量或源信息（如果可用）。

## <a name="sample"></a>示例

有关如何使用此命名空间和对象以及如何使用的端到端示例，请参阅 GitHub 上的[CodeFlow](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)示例。

## <a name="object-methods"></a>对象方法

|名称|返回类型|签名|描述|
|--- |--- |--- |--- |
|CreateDisassembler| [拆装](dbgmodel-object-disassembler.md)|CreateDisassembler （[体系结构]）|创建指定体系结构的拆装器对象。 体系结构可以是 "ARM"、"ARM64"、"X64" 或 "X86"。 如果未指定体系结构，则假定为 X64。 |
|TraceDataFlow|[指令](dbgmodel-object-instruction.md)[集合](dbgmodel-namespace-collections.md)|TraceDataFlow （[address]）|查看指定*地址*处的指令（如果未指定任何地址，则查看当前指令指针）及其所有源操作数。 此方法向后遍历函数的控制流，查找影响跟踪指令的源操作数的任何指令。 **此方法需要加载在[CodeFlow.js 示例](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)中找到的 CodeFlow 扩展。**|

## <a name="remarks"></a>备注

默认情况下，CreateDisassembler 默认为 "X64"，在某个时候，此行为将更改以在当前线程的指令指针上提取模块的体系结构。
