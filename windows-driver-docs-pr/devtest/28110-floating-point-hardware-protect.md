---
title: C28110
description: 警告 C28110 驱动程序必须保护浮点硬件状态。 请参阅使用浮点型。
ms.assetid: 2f6045e3-92b2-4773-a8de-3d0ec09c5d31
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28110
ms.openlocfilehash: 8e5ed2c55c69a77510133ffc9b606577adada1ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565739"
---
# <a name="c28110"></a>C28110


警告 C28110:驱动程序必须保护浮点硬件状态。 请参阅使用 float

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>使用<strong>KeSaveFloatingPointState</strong>并<strong>KeRestoreFloatingPointState</strong>围绕浮点运算。 显示驱动程序应使用相应<strong>eng...</strong>例程。</p></td>
</tr>
</tbody>
</table>

 

此警告才在内核模式下适用。 该驱动程序尝试时要使用的变量或常数浮点类型的代码不受[ **KeSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff553243)并[ **KeRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff553185)，或[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)并[ **EngRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565006).

通常情况下，驱动程序运行与最新应用程序和任何使用不受的浮动点的浮点上下文[ **KeSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff553243)和[ **KeRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff553185)可以更改其他进程的结果并通常会在驱动程序导致不正确或意外的结果。

显示驱动程序应使用[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)并[ **EngRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff565006)。

此错误的实例检测到任何特定流路径后，代码分析工具会隐藏后续类似错误。 代码分析工具不会报告函数定义的采用浮点类型自变量或返回浮点类型，此错误，因为调用方将报告使用。

程序将保存并还原浮点状态周围函数调用和被调用的函数执行浮点运算时，可以在错误会触发此警告。

如果函数有意设计成使用浮点运算，并希望其中浮点数安全的情况下在上下文中调用，应批注与函数**\_内核\_float\_使用\_**. 此批注将禁止显示警告函数体中的并会导致要检查调用安全地保护浮点操作的调用上下文。 如果浮点运算出现在参数或返回值时，效果等同于使用**\_内核\_float\_使用\_**。

通过使用**\_内核\_float\_使用\_** 上 （或添加相应的保存和还原对的调用） 的所有函数中使用浮动都点直到没有任何警告，驱动程序可以有保证的不恰当使用浮点硬件的免费。 有关详细信息，请参阅[驱动程序的浮动点批注](floating-point-annotations-for-drivers.md)。

 

 





