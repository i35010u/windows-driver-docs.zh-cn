---
title: 了解跟踪树窗格
description: 了解跟踪树窗格
ms.assetid: 98640d7e-29fc-4397-ac6b-47f4e17f88a1
keywords:
- 静态驱动程序验证工具报表 WDK，跟踪树窗格
- 跟踪树窗格 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bad7e81607d18d05e2ee4c487062a3b8a5430eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562891"
---
# <a name="understanding-the-trace-tree-pane"></a>了解跟踪树窗格


**跟踪树**窗格是缺陷查看器的焦点。 通常情况下，单步执行中的代码**跟踪树**窗格中的，同时注意代码在其效果**源代码**窗格中的值在**状态**窗格。

**跟踪树**窗格分为一系列可展开和折叠节点的分层结构。 在层次结构指示导致要执行的其他元素的代码元素。 此格式可帮助你解释每个代码分支和显示和单步执行跟踪时轻松地隐藏代码节。

下面的屏幕截图显示了一个示例**跟踪树**窗格。

![跟踪树窗格中的缺陷查看器的屏幕截图](images/sdv-tracetree.png)

在每个代码元素**跟踪树**窗格会跟有它的源文件中的行编号。 此编号，可帮助你在源树窗口和源代码文件中找到的代码元素。

中的代码的某些行**源代码**窗格中的多个元素与对应**跟踪树**窗格。 代码行导致多个操作，则会发生这种情况。 例如，如果函数调用参数为 IRQL，包括函数调用的代码行还可能包括执行调用以找到当前 irql，因此，例如：

```
IoReleaseCancelSpinLock(KeGetCurrentIrql());
```

在此情况下，**跟踪树**窗格将包括的一个关键因素[ **KeGetCurrentIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552054)函数调用，几个调用的 SDV 操作系统模型随机生成 irql，因此，然后调用[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550)返回 IRQL 与。

 

 





