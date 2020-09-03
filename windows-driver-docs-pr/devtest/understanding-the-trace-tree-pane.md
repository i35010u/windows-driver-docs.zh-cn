---
title: 了解跟踪树窗格
description: 了解跟踪树窗格
ms.assetid: 98640d7e-29fc-4397-ac6b-47f4e17f88a1
keywords:
- 静态驱动程序验证器报表 WDK，跟踪树窗格
- 跟踪树窗格 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 889dc7f762f4c587c3a5e7a286c699bd593adc14
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384879"
---
# <a name="understanding-the-trace-tree-pane"></a>了解跟踪树窗格


" **跟踪树** " 窗格是缺陷查看器的焦点。 通常，您在 **跟踪树** 窗格中单步执行代码，同时在 " **源代码** " 窗格和 " **状态** " 窗格中的值上观察其代码效果。

**跟踪树**窗格使用一系列可展开和可折叠的节点组织为一个层次结构。 层次结构指示导致执行其他元素的代码元素。 此格式可帮助你解释每个代码分支，并在逐句通过跟踪时轻松显示和隐藏代码段。

下面的屏幕截图显示了一个示例 **跟踪树** 窗格。

![缺陷查看器中 "跟踪树" 窗格的屏幕截图](images/sdv-tracetree.png)

**跟踪树**窗格中的每个代码元素前面都带有其在源文件中的行号。 此编号有助于在源树窗口和源文件中查找代码元素。

" **源代码** " 窗格中的一些代码行对应于 " **跟踪树** " 窗格中的多个元素。 当代码行导致多个操作时，会发生这种情况。 例如，如果函数调用参数为 IRQL，则包括函数调用的代码行还可能包括调用以查找当前的 IRQL，如：

```
IoReleaseCancelSpinLock(KeGetCurrentIrql());
```

在这种情况下，" **跟踪树** " 窗格将包含 [**KeGetCurrentIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kegetcurrentirql) 函数调用的关键元素、对 SDV 操作系统模型的几次调用以随机生成 irql，然后使用返回的 irql 调用 [**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 。

 

