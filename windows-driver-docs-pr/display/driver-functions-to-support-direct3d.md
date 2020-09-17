---
title: 用于支持 Direct3D 的驱动程序函数
description: 用于支持 Direct3D 的驱动程序函数
ms.assetid: 949551c3-2172-454c-b398-eba468b90705
keywords:
- Direct3D WDK Windows 2000 显示，功能
- 功能 WDK Direct3D
- 回调函数 WDK Direct3D
- LPD3DHAL_MYFUNCTIONDATA
- D3DHAL_MYFUNCTIONDATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 961243fd4b5c178cbc2c20dfd349b7d2fcddc23e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716510"
---
# <a name="driver-functions-to-support-direct3d"></a>用于支持 Direct3D 的驱动程序函数


## <span id="ddk_driver_functions_to_support_direct3d_gg"></span><span id="DDK_DRIVER_FUNCTIONS_TO_SUPPORT_DIRECT3D_GG"></span>


支持 Direct3D 的驱动程序提供 Direct3D 回调函数和 DirectDraw DDI 函数。 Direct3D DDI 回调的原型如下所示：

```cpp
typedef DWORD (APIENTRY *LPD3DHAL_MYFUNCTIONCB) (LPD3DHAL_MYFUNCTIONDATA);
```

在前面的语法中：

-   LPD3DHAL \_ MYFUNCTIONCB 指向可被称为 *MyFunction*的驱动程序实现的回调。 所有回叫名称由显示驱动程序编写器 pseudonames 决定。

-   LPD3DHAL \_ MYFUNCTIONDATA 是指向 \_ 传递到回调的 D3DHAL MYFUNCTIONDATA 结构的指针。 回调参数结构的特征如下：
    -   每个结构 **dwhContext**的第一个成员都是上下文句柄，用于描述回调应在其中运行的三维上下文。 此规则的唯一例外是 D3DHAL \_ CONTEXTCREATEDATA 结构。
    -   每个结构的最后一个成员是 **ddrval**。 此成员用于将回调的返回值传递回 Direct3D，以便可以将其返回给调用应用程序。

若要确定如何初始化 Direct3D 回叫函数，请参阅 [Direct3d 驱动程序初始化](direct3d-driver-initialization.md)。

下表列出了在 Direct3D 驱动程序中实现的 Direct3D 回叫函数。 除 [**D3dValidateTextureStageState**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)外，所有回调函数都是必需的，这是可选的，具体取决于硬件功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb" data-raw-source="[&lt;strong&gt;D3dContextCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)"><strong>D3dContextCreate</strong></a></p></td>
<td align="left"><p>创建上下文。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb" data-raw-source="[&lt;strong&gt;D3dContextDestroy&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)"><strong>D3dContextDestroy</strong></a></p></td>
<td align="left"><p>销毁上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a></p></td>
<td align="left"><p>创建纹理控点和图面之间的关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_destroyddlocal" data-raw-source="[&lt;strong&gt;D3dDestroyDDLocal&lt;/strong&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)"><strong>D3dDestroyDDLocal</strong></a></p></td>
<td align="left"><p>销毁先前由 <a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a> 创建的、属于同一给定本地 DirectDraw 对象的所有 Direct3D 图面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb" data-raw-source="[&lt;strong&gt;D3dDrawPrimitives2&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)"><strong>D3dDrawPrimitives2</strong></a></p></td>
<td align="left"><p>呈现基元，并将更新的状态返回到 Direct3D。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverstate" data-raw-source="[&lt;strong&gt;D3dGetDriverState&lt;/strong&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverstate)"><strong>D3dGetDriverState</strong></a></p></td>
<td align="left"><p>返回 DirectDraw 和 Direct3D 运行时驱动程序的状态信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb" data-raw-source="[&lt;strong&gt;D3dValidateTextureStageState&lt;/strong&gt;](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)"><strong>D3dValidateTextureStageState</strong></a></p></td>
<td align="left"><p>执行纹理阶段状态验证，这是所有支持纹理的驱动程序所必需的。</p></td>
</tr>
</tbody>
</table>

 

若要支持 Direct3D，驱动程序必须最少支持 Microsoft DirectDraw，并且还必须实现某些 DirectDraw DDI 函数。 下表列出了与 Direct3D 支持相关的功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo" data-raw-source="[&lt;strong&gt;DrvGetDirectDrawInfo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)"><strong>DrvGetDirectDrawInfo</strong></a></p></td>
<td align="left"><p>此函数检索图形硬件的功能。 在此初始化函数中，驱动程序指示它支持 Direct3D。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>DdGetDriverInfo</strong></a></p></td>
<td align="left"><p>运行时通过 Guid 查询此回调函数以获取有关驱动程序的其他信息。 一些 Guid 专用于驱动程序的 Direct3D 支持。</p></td>
</tr>
</tbody>
</table>

 

[Directdraw 中讨论](directdraw.md)了 directdraw 函数和回调实现的详细信息。

