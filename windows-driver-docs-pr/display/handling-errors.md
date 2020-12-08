---
title: 处理错误
description: 处理错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 947faff057a160d849136e781cd0ddb7a93ccd4d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819113"
---
# <a name="handling-errors"></a>处理错误


用户模式显示驱动程序实现的 [Direct3D 版本10函数](/windows-hardware/drivers/ddi/index) 对于返回参数类型通常具有 VOID。 此规则的主要例外情况是 * CalcPrivate ***ObjType**_Size_-type 函数 (例如， [**CalcPrivateResourceSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize) 函数) 。 这种类型的函数返回一个大小 \_ T 参数类型，该类型指示驱动程序通过 * Create ***ObjType** 函数创建特定对象类型所需的内存区域的大小， (例如， [**CreateResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) 。

返回 VOID 可防止用户模式显示驱动程序通过用户模式显示驱动程序的函数返回参数) 以传统 (方式通知 Direct3D 运行时错误。 相反，用户模式显示驱动程序必须使用 Direct3D 运行时的 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) 回调函数将此类信息传递回运行时。 运行时提供指向其在 [**D3D10DDI \_ CORELAYER \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构中的 **pfnSetErrorCb** 的指针，pUMCallbacks [**\_ D3D10DDIARG**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的 **CREATEDEVICE** 成员在调用 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数时指向该结构。

每个用户模式显示驱动程序函数的 "引用" 页指定函数可以通过调用 **pfnSetErrorCb** 传递的错误。 这意味着，如果用户模式显示驱动程序使用当前用户模式显示驱动程序函数不允许的错误代码调用 **pfnSetErrorCb** ，则运行时将确定错误条件是关键的并正确操作。 由于运行时将在 **pfnSetErrorCb** 过程中适当地操作，因此您不应希望 **pfnSetErrorCb** \_ 通过调用 **pfnSetErrorCb** ( S OK ) 等操作来撤消调用 pfnSetErrorCb ( E ) 的影响 \_ 。 事实上，运行时确定 S OK 与 \_ E FAIL 相同或严重 \_ 。 S \_ OK 返回代码的概念等效于用户模式显示驱动程序函数根本不会调用 **pfnSetErrorCb** 。

如果 Direct3D 运行时确定错误情况非常重要，它将首先通过使用 Dr. Watson 记录错误来采取措施，即默认的事后 (实时) 调试器。 然后，运行时将失去设备的用途，从而模拟接收 D3DDDIERR \_ DEVICEREMOVED 错误代码的方案。 通过要求驱动程序调用 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) 回调函数，可能会有很大的几率，因为驱动程序的每个错误都将有一个与之关联的有用调用堆栈。 如果调用堆栈与错误关联，则会启用快速诊断和准确的 Dr. Watson 日志。

如果驱动程序中出现问题，则应在驱动程序代码中使用 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) ，即使返回的错误代码是运行时不允许用于特定驱动程序函数的，由运行时确定为驱动程序 bug 或问题。 更糟的是，用户模式显示驱动程序要吸收严重错误并继续。 用户模式显示驱动程序应尽可能接近错误检测点的 **pfnSetErrorCb** ，以提供用于事后调试的有用调用堆栈。

下表列出了 Direct3D 运行时允许从特定驱动程序函数进行的错误类别。

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
<td align="left"><p>驱动程序不应遇到任何错误，包括 D3DDDIERR_DEVICEREMOVED。 运行时将确定对 <a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb" data-raw-source="[&lt;strong&gt;pfnSetErrorCb&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)"><strong>pfnSetErrorCb</strong></a> 的任何调用都是重要的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDeviceRemoved</p></td>
<td align="left"><p>除了 D3DDDIERR_DEVICEREMOVED 之外，驱动程序不应遇到任何错误。 运行时将确定对未通过 D3DDDIERR_DEVICEREMOVED 的 <strong>pfnSetErrorCb</strong> 的任何调用都是重要的。 如果设备已被删除，则无需驱动程序即可返回 DEVICEREMOVED。 但是，运行时允许驱动程序返回 DEVICEREMOVED （如果 DEVICEREMOVED 干扰就具有驱动程序函数），这通常不会发生。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowOutOfMemory</p></td>
<td align="left"><p>驱动程序可能会耗尽内存。 因此，该驱动程序可以通过 <strong>pfnSetErrorCb</strong>传递 E_OUTOFMEMORY 和 D3DDDIERR_DEVICEREMOVED。 运行时将确定任何其他错误代码都是关键代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowCounterCreationErrors</p></td>
<td align="left"><p>驱动程序可能会耗尽内存。 驱动程序还可能无法创建计数器，因为存在独占的计数器性质。 因此，该驱动程序可以通过 <strong>pfnSetErrorCb</strong>传递 E_OUTOFMEMORY、DXGI_DDI_ERR_NONEXCLUSIVE 和 D3DDDIERR_DEVICEREMOVED。 运行时将确定任何其他错误代码都是关键代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowMapErrors</p></td>
<td align="left"><p>驱动程序应检查资源争用情况。 因此，如果 D3D10_DDI_MAP_FLAG_DONOTWAIT 标志传递到驱动程序的<a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap" data-raw-source="[&lt;strong&gt;ResourceMap&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)"><strong>windows.applicationmodel.resources.core.resourcemap</strong></a>函数，则驱动程序可以通过<strong>pfnSetErrorCb</strong>传递 DXGI_DDI_ERR_WASSTILLDRAWING。 驱动程序还可以通过 <strong>pfnSetErrorCb</strong>传递 D3DDDIERR_DEVICEREMOVED。 运行时将确定任何其他错误代码都是关键代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowGetDataErrors</p></td>
<td align="left"><p>驱动程序应检查查询是否已完成。 因此，如果查询尚未完成，则驱动程序可以通过 <strong>pfnSetErrorCb</strong> 传递 DXGI_DDI_ERR_WASSTILLDRAWING。 驱动程序还可以通过 <strong>pfnSetErrorCb</strong>传递 D3DDDIERR_DEVICEREMOVED。 运行时将确定任何其他错误代码都是关键代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AllowWKCheckCounterErrors</p></td>
<td align="left"><p>驱动程序的 <a href="/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter" data-raw-source="[&lt;strong&gt;CheckCounter&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkcounter)"><strong>CheckCounter</strong></a> 函数应指示它是否支持运行时定义的任何计数器。 因此，该驱动程序可以通过 <strong>pfnSetErrorCb</strong>传递 DXGI_DDI_ERR_UNSUPPORTED。 运行时将确定任何其他错误代码都是关键代码。</p>
<p>驱动程序无法返回任何检查类型函数的 D3DDDIERR_DEVICEREMOVED。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AllowDDCheckCounterErrors</p></td>
<td align="left"><p>驱动程序应该验证与设备相关的计数器标识符 (计数器 ID) ，以确保计数器 ID 在范围内，并且有足够的空间将每个计数器字符串复制到提供的缓冲区中。 当参数不正确时，驱动程序可以通过 <strong>pfnSetErrorCb</strong>传递 E_INVALIDARG。</p>
<p>驱动程序无法返回任何检查类型函数的 D3DDDIERR_DEVICEREMOVED。</p></td>
</tr>
</tbody>
</table>

 

