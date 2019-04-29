---
title: 调试器数据模型 - 控制流对象
description: 对于完全分析反汇编，每个基本块包含一组控制流对象。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b410b04de5f2ad5172bbd1c3fe85498ac71c6f28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374389"
---
# <a name="control-flow-objects"></a>控制流对象 
## <a name="summary"></a>总结
对于完全分析反汇编，每个`basic block`包含一组 InboundControlFlows 和 OutboundControlFlows 属性中的控制流对象。
## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|LinkedBlock|该链接另一端上的基本块对象。 如果这是有入站的控制流，这是指，必须将分支指令的基本块。 如果这是出站控制流，这表示它是分支指令的目标的基本块。|
|LinkKind|指示哪种控制流导致两个块之间的链接 (例如："FallThrough"或者"分支"）。|
|SourceInstruction|控制流链接的源。 这是将分支指令或基本块中的最后一个指令。|
|TargetInstruction|控制流链接的目标。 这是分支目标或之后具有贯穿的基本块的最后一个指令的指令。|