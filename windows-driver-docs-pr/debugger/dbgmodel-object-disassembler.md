---
title: 调试器数据模型 - 拆装器对象
description: 拆装器对象启用反汇编代码的特定体系结构的功能。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9bd54cb1aafc31f42cbf39f5cfa36db4fa6cbf97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374367"
---
# <a name="disassembler-objects"></a>拆装器对象
## <a name="summary"></a>总结
拆装器对象启用反汇编代码的特定体系结构的功能。
## <a name="object-methods"></a>对象方法
|名称|返回类型|签名|描述|
|--- |--- |--- |--- |
|DisassembleBlocks|[集合](dbgmodel-namespace-collections.md)的[基本块](dbgmodel-object-basic-block.md)|DisassembleBlocks(address)|开始在拆装*地址*，并返回[集合](dbgmodel-namespace-collections.md)的基本块。 反汇编此处从是以线性方式进*地址*按指令的指令。 由于这不执行完整流分析的函数时，它是完全有可能，可能跳转到此方法返回的块的中间。 仅有一个出口点从每个;但是。|
|DisassembleInstructions|[集合](dbgmodel-namespace-collections.md)的[指令](dbgmodel-object-instruction.md)|DisassembleInstructions(address)|开始在拆装*地址*。 |
|DisassembleFunction|[集合](dbgmodel-namespace-collections.md)的[基本块](dbgmodel-object-basic-block.md)|DisassembleFunction(address)|假设一个函数开始*地址*，此执行该函数的完整流分析。 结果是[集合](dbgmodel-namespace-collections.md)的基本块具有一个入口点和一个退出点。|
|GetRegister|[register](dbgmodel-object-register.md)|GetRegister(regId)|返回从给定的注册 id 注册对象。|
## <a name="remarks"></a>备注
此处提供的拆装器具有明显优于反汇编输出存在已拆装的函数的完整符号信息时 (例如： 它将使用新的地址和操作数的大小，以确定被触摸的结构/联合中的哪些字段)。

拆装器的给定的实例可以缓存大量数据，以便提供更好的体验。