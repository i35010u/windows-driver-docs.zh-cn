---
title: Production 模板指令
description: Production 模板指令
ms.assetid: 5deae299-389a-4de4-8f2f-7c247f045ada
keywords:
- 生产指令 WDK GDL
- 构造 WDK GDL，有效的组合
- 模板 WDK GDL，主机模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b133b7a79d2590e8895606939c5f2d32d39dfe10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354558"
---
# <a name="production-template-directive"></a>Production 模板指令


\*生产模板指令指定的特定构造中可以出现的成员的有效组合。 此指令可以出现仅在使用的模板内\*类型：构造。

如果存在此指令，则针对每个实例绑定到的生产主机模板构造计算生产。 主机模板是包含生产指令的模板。 如果生产指令的计算结果为**FALSE**，发出一条警告消息，但处理在其他方面不受影响。 如果主机模板包含没有生产指令，不执行任何验证。

\*生产指令出现主机模板构造的根级别。 如果多个\*生产指令出现在根级别，将计算仅最新定义的指令。 评估生产指令的结果是一个布尔值。

\*生产指令本身就是一种构造。 子元素\*生产指令是任一另\*生产构造或\*成员构造或这两个 （也称为的子生产） 的组合。 不能使用中的命名空间指令\*生产指令。

包含在每个子级生产\*生产指令还可以计算为**TRUE**或**FALSE**。 第一个评估每个及其子生产将评估生产指令。 封闭的父生产指令的结果是通过执行获得的结果的每个子级生产上的简单逻辑操作。 要应用的逻辑操作的类型由的 vValue 指定\*生产指令。

值\*生产指令可以是以下符号之一：完全\_一个，SATISFY\_所有，或在\_最低\_之一。

下面的示例显示了生产指令。

```cpp
*Production: EXACTLY_ONE
{   ... child Productions ... }
```

使用以下算法定义生产指令值：

1.  如果生产精确指定\_一个此生产计算结果为**TRUE**如果只有一个子生产的计算结果为**TRUE**，而剩下的**FALSE**. 否则，在生产的计算结果为**FALSE**。

2.  如果生产环境指定 SATISFY\_所有，此生产的计算结果为**TRUE**仅当所有子生产计算结果为**TRUE**。 否则，在生产的计算结果为**FALSE**。

3.  如果生产环境指定 AT\_至少\_此生产的一个计算结果为**TRUE**如果至少一个或多个子生产计算结果为**TRUE**。 否则，在生产的计算结果为**FALSE**。

\*生产指令可以嵌套到任意深度。

 

 




