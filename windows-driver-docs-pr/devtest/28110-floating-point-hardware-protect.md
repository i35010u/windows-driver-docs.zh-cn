---
title: C28110
description: 警告 C28110 驱动程序必须保护浮点硬件状态。 请参阅使用 float。
ms.assetid: 2f6045e3-92b2-4773-a8de-3d0ec09c5d31
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28110
ms.openlocfilehash: 13448082e60bf8a8a33d3b7768039dc4c5df3087
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839603"
---
# <a name="c28110"></a>C28110


警告 C28110：驱动程序必须保护浮点硬件状态。 请参阅使用 float

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>围绕浮点运算使用<strong>KeSaveFloatingPointState</strong>和<strong>KeRestoreFloatingPointState</strong> 。 显示驱动程序应使用相应的<strong>Eng ...</strong>例程。</p></td>
</tr>
</tbody>
</table>

 

此警告仅适用于内核模式。 当代码不是由[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)和[**KeRestoreFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)、 [**EngSaveFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)和[**保护时，驱动程序尝试使用 float 类型的变量或常量EngRestoreFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)。

通常，驱动程序使用最新应用程序的浮点上下文运行，并且任何不受[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)和[**KeRestoreFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)保护的浮点的使用都可以更改其他处理和通常会导致驱动程序中出现不正确或意外的结果。

显示驱动程序应使用[**EngSaveFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)和[**EngRestoreFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)。

沿任何特定流路径检测到此错误的实例后，代码分析工具将取消后续的类似错误。 对于采用浮点类型参数或返回浮动类型的函数定义，代码分析工具不会报告此错误，因为调用方将报告使用。

当程序在调用函数时保存和还原浮点状态，并且被调用函数执行浮点运算时，可能会错误地触发此警告。

如果函数有意使用浮点运算，并且期望在浮点安全的上下文中调用，则应使用 **\_\_内核\_float\_** 批注该函数。 此批注将禁止显示函数体中的警告，并导致调用上下文检查调用是否安全地受到浮点运算的保护。 如果在参数或返回值中出现浮点运算，则效果与使用 **\_使用\_内核\_float\_** 相同。

通过使用 **\_内核\_float\_使用\_** on （或添加对的适当的保存和还原调用）所有使用浮点的函数直到不会出现任何警告，可以确保驱动程序无需使用浮点软. 有关详细信息，请参阅[驱动程序的浮点批注](floating-point-annotations-for-drivers.md)。

 

 





