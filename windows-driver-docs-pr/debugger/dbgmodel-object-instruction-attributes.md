---
title: 调试器数据模型-指令特性的对象
description: 包含一些指令的详细信息的说明。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8687a5eb0606fe7c633f5b7e6e1ad5ff0303e5c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524594"
---
# <a name="instruction-attributes-objects"></a>指令特性的对象 
## <a name="summary"></a>摘要
*特性*的属性[指令](dbgmodel-object-instruction.md)对象包含的某些指令的详细信息的说明。
## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|IsBranch|指示该指令是否为任何类型的分支指令。|
|IsConditional|指示是否为条件指令的结果 (例如： 条件分支)。|
|IsCall|指示该指令是否为任何类型的调用指令。|
|IsReturn|指示该指令是否为任何类型的返回指令。|