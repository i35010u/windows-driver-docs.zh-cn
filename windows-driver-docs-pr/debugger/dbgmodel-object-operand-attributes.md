---
title: 调试器数据模型-操作数属性对象
description: 由操作数属性对象描述的机器指令的操作数。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5d8cd8b7a0915f07de8fb5748aee06ab3afbc5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547473"
---
# <a name="operand-attributes-objects"></a>操作数属性对象 
## <a name="summary"></a>摘要
由操作数属性对象描述的机器指令的操作数。
## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|HasImmediate|指示是否在操作数具有即时值作为操作数的一部分。|
|IsInput|指示的操作数是否指令 （对任何 does 指令的输入） 的数据源。|
|IsOutput|指示的操作数是否指令 （指令执行的任何内容的输出） 的数据目标。|
|IsMemoryReference|指示的操作数是否内存引用。|
|IsImmediate|指示的操作数是否即时值。 此类操作数，则还有*HasImmediate*设置为 true。|
|IsRegister|指示的操作数是否只是寄存器。|