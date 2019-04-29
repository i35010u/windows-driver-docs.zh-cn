---
title: 处理错误
description: 处理错误
ms.assetid: ac4e056e-3304-4934-887a-5cc2b87989bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b602d001d8e617b2151e4060061eb1bd427ef8e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323719"
---
# <a name="handling-errors"></a>处理错误


[Direct3D 版本 10 函数](https://msdn.microsoft.com/library/windows/hardware/ff552909)，用户模式显示驱动程序实现通常具有 VOID 返回参数类型。 此规则的主要例外是*CalcPrivate***ObjType***大小*-类型函数 (例如， [ **CalcPrivateResourceSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538302)函数)。 此类函数返回一个大小\_T 参数类型，该值指示驱动程序需要用于创建通过特定对象类型的内存区域的大小 * 创建 ***ObjType**-类型 （适用于函数示例中， [ **CreateResource(D3D10)**](https://msdn.microsoft.com/library/windows/hardware/ff540691))。

返回 VOID 可防止用户模式显示驱动程序通知错误 Direct3D 运行中的传统方法 （即，通过用户模式显示驱动程序的函数返回参数）。 相反，用户模式显示驱动程序必须使用 Direct3D 运行时[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)将此类信息传递回运行时的回调函数。 在运行时提供一个指向其**pfnSetErrorCb**中[ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff541820)结构的**pUMCallbacks**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)结构在调用指向[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)函数。

每个用户模式显示驱动程序函数的参考页指定错误的函数可以通过调用**pfnSetErrorCb**。 这意味着，如果用户模式显示驱动程序调用**pfnSetErrorCb**并不允许使用当前用户模式显示驱动程序函数返回错误代码，运行时确定错误条件至关重要，作用适当地。 因为运行时将采取相应措施期间**pfnSetErrorCb**，不应期望可以反转调用的效果**pfnSetErrorCb**(E\_失败) 通过调用类似于**pfnSetErrorCb**(S\_确定)。 事实上，运行时确定的 S\_确定是只是作为无效或关键为 E\_失败。 S 的概念\_确定返回代码是否等效于用户模式显示驱动程序函数不调用**pfnSetErrorCb**根本。

如果 Direct3D 运行时确定严重错误条件，将通过将错误记录到灾难恢复首先需要操作。Watson-默认事后 （实时） 调试器。 在运行时将丢失设备目标，从而模拟以下场景： 接收 D3DDDIERR 的\_DEVICEREMOVED 错误代码。 通过要求驱动程序来调用[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)回调函数，您可能已变得更来自驱动程序的每个错误，将具有与之关联的有用的调用堆栈。 具有与错误关联的调用堆栈，快速诊断和准确的灾难恢复。Watson 记录。

应使用[ **pfnSetErrorCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568929)即使返回运行时不允许特定的驱动程序函数的错误代码出现在您的驱动程序问题时在驱动程序代码中由运行时作为驱动程序 bug 或问题。 它将会更严重的用户模式显示驱动程序，absorb 严重错误并继续。 用户模式显示驱动程序应调用**pfnSetErrorCb**靠近错误检测，以提供有用的调用堆栈进行事后调试的点。

下表列出了 Direct3D 运行时允许从特定的驱动程序函数的错误的类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误类别</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NoErrors</p></td>
<td align="left"><p>该驱动程序应该不会遇到任何错误，包括 D3DDDIERR_DEVICEREMOVED。 在运行时将确定任何对<a href="https://msdn.microsoft.com/library/windows/hardware/ff568929" data-raw-source="[&lt;strong&gt;pfnSetErrorCb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568929)"> <strong>pfnSetErrorCb</strong> </a>至关重要。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDeviceRemoved</p></td>
<td align="left"><p>该驱动程序应该不会遇到任何错误，但 D3DDDIERR_DEVICEREMOVED 除外。 在运行时将确定任何对<strong>pfnSetErrorCb</strong>器不传递 D3DDDIERR_DEVICEREMOVED 至关重要。 该驱动程序不需要返回 DEVICEREMOVED，如果删除该设备。 但是，在运行时将允许驱动程序返回 DEVICEREMOVED，以防 DEVICEREMOVED 干扰通常不应发生情况的驱动程序函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowOutOfMemory</p></td>
<td align="left"><p>内存不足可能是可以运行的驱动程序。 因此，该驱动程序可以传递 E_OUTOFMEMORY 和通过 D3DDDIERR_DEVICEREMOVED <strong>pfnSetErrorCb</strong>。 在运行时将确定任何其他错误代码是关键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowCounterCreationErrors</p></td>
<td align="left"><p>内存不足可能是可以运行的驱动程序。 该驱动程序还可能无法创建由于排他性质计数器的计数器。 因此，该驱动程序可以将传递 E_OUTOFMEMORY、 DXGI_DDI_ERR_NONEXCLUSIVE，并通过 D3DDDIERR_DEVICEREMOVED <strong>pfnSetErrorCb</strong>。 在运行时将确定任何其他错误代码是关键。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowMapErrors</p></td>
<td align="left"><p>该驱动程序应检查资源争用。 因此，可以将驱动程序传递通过 DXGI_DDI_ERR_WASSTILLDRAWING <strong>pfnSetErrorCb</strong> D3D10_DDI_MAP_FLAG_DONOTWAIT 标志传递到驱动程序的<a href="https://msdn.microsoft.com/library/windows/hardware/ff569492" data-raw-source="[&lt;strong&gt;ResourceMap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569492)"> <strong>ResourceMap</strong> </a>函数。 该驱动程序还可以传递通过 D3DDDIERR_DEVICEREMOVED <strong>pfnSetErrorCb</strong>。 在运行时将确定任何其他错误代码是关键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowGetDataErrors</p></td>
<td align="left"><p>该驱动程序应检查完成查询。 因此，可以将驱动程序传递通过 DXGI_DDI_ERR_WASSTILLDRAWING <strong>pfnSetErrorCb</strong>如果查询尚未完成。 该驱动程序还可以传递通过 D3DDDIERR_DEVICEREMOVED <strong>pfnSetErrorCb</strong>。 在运行时将确定任何其他错误代码是关键。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowWKCheckCounterErrors</p></td>
<td align="left"><p>在驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/ff539385" data-raw-source="[&lt;strong&gt;CheckCounter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539385)"> <strong>CheckCounter</strong> </a>函数应指示它是否支持任何运行时定义的计数器。 因此，可以将驱动程序传递通过 DXGI_DDI_ERR_UNSUPPORTED <strong>pfnSetErrorCb</strong>。 在运行时将确定任何其他错误代码是关键。</p>
<p>该驱动程序不能为任何检查类型函数返回 D3DDDIERR_DEVICEREMOVED。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDDCheckCounterErrors</p></td>
<td align="left"><p>驱动程序应验证依赖于设备的计数器标识符 (计数器 ID)，以确保计数器 ID 范围内并且没有足够的空间来将每个计数器字符串复制到提供的缓冲区。 该驱动程序可以将传递通过 E_INVALIDARG <strong>pfnSetErrorCb</strong>，当该参数不正确以这种方式。</p>
<p>该驱动程序不能为任何检查类型函数返回 D3DDDIERR_DEVICEREMOVED。</p></td>
</tr>
</tbody>
</table>

 

 

 





