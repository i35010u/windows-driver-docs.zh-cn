---
title: 调试器数据模型 - 实时变量对象
description: 这是该特定的指令处实时和它们的位置的变量信息的集合
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c228ccd00d97693462a94e6f96589513e889e7b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376081"
---
# <a name="live-variable-objects"></a>活动变量的对象 
## <a name="summary"></a>总结
具有完整符号信息时，每个指令包含的变量，这是该特定的指令处实时和它们的位置信息的集合。
## <a name="object-properties"></a>对象属性
|名称|描述|
|--- |--- |
|LocationKind|描述变量存储中的位置的种类的字符串 (例如："注册"，"RegisterRelative"，等等...)|
|偏移量|从存储在变量的位置的偏移量。 在 [rbp + 8]，例如存储的变量，偏移量将是 8。|
|注册|一个[注册](dbgmodel-object-register.md)介绍寄存器变量的存储位置或相对于的对象。|
|VariableName|要描述变量的名称。|