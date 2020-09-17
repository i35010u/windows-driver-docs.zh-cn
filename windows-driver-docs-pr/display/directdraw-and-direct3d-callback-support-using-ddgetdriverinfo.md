---
title: 使用 DdGetDriverInfo 的 DirectDraw 和 D3D 回调支持
description: 显示驱动程序可以实现 DdGetDriverInfo 函数，以指示各种 DirectDraw 和 Direct3D 回调支持。
ms.assetid: 7054564e-4520-4900-946a-95c92908667c
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- 回调函数 WDK DirectDraw
- DdGetDriverInfo
- Direct3D WDK Windows 2000 显示，回调
- 回调函数 WDK Direct3D
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，回调函数
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ae8b88c113dd769b7568b727120f03324c751be7
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716516"
---
# <a name="directdraw-and-direct3d-callback-support-using-ddgetdriverinfo"></a>使用 DdGetDriverInfo 的 DirectDraw 和 Direct3D 回调支持

显示驱动程序可以实现 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 函数，以指示各种 DirectDraw 和 Direct3D 回调支持。 回调支持是由驱动程序在[**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**guidInfo**成员中接收到的、 *lpGetDriverInfo*参数指向的 guid。 驱动程序返回指向 **lpvData** 成员中的结构的指针，该结构指定 DirectDraw 或 Direct3D 回叫支持。

- 如果驱动程序收到 GUID \_ COLORCONTROLCALLBACKS guid，则返回指向 [**DD \_ ColorControlCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks) 结构的指针。 如果支持 [颜色控制](color-control-initialization.md)，驱动程序将填充 DD COLORCONTROLCALLBACKS 的 **ColorControl** 成员， \_ 以指定其 [*DdControlColor*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol) 回调函数。

- 如果驱动程序收到 GUID \_ D3DCallbacks、guid \_ D3DCALLBACKS3 或 GUID \_ Miscellaneous2Callbacks guid，它将返回指向 [**D3DHAL \_ 回调**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks)、 [**D3DHAL \_ CALLBACKS3**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks3)或 [**DD \_ Miscellaneous2Callbacks**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks) 结构的指针。 驱动程序使用这些结构来指示其 [Direct3D 回叫支持](driver-functions-to-support-direct3d.md)。 有关详细信息，请参阅 [DIRECT3D DDI](direct3d.md)。

- 如果驱动程序收到 GUID \_ KERNELCALLBACKS guid，则返回指向 [**DD \_ KernelCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-dd_kernelcallbacks) 结构的指针。 驱动程序将填充 DD KERNELCALLBACKS 的成员， \_ 以指示它支持以下回调函数。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">回调函数</th>
  <th align="left">说明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface" data-raw-source="[&lt;em&gt;DdSyncSurfaceData&lt;/em&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface)"><em>DdSyncSurfaceData</em></a></p></td>
  <td align="left"><p>设置和修改表面数据。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport" data-raw-source="[&lt;em&gt;DdSyncVideoPortData&lt;/em&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)"><em>DdSyncVideoPortData</em></a></p></td>
  <td align="left"><p> (VPE) 对象数据设置和修改视频端口扩展。</p></td>
  </tr>
  </tbody>
  </table>

- 如果驱动程序收到 GUID \_ MISCELLANEOUSCALLBACKS guid，则返回指向 [**DD \_ MiscellaneousCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_miscellaneouscallbacks) 结构的指针。 如果它支持 [*DdGetAvailDriverMemory*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory) 回调函数，则驱动程序将填充 DD MISCELLANEOUSCALLBACKS 的 *DdGetAvailDriverMemory* 成员 \_ 以指定 *DdGetAvailDriverMemory*。

- 如果驱动程序收到 GUID \_ MOTIONCOMPCALLBACKS guid，它将返回一个指向 [**DD \_ MotionCompCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks) 结构的指针，以指示其对 [运动补偿回调](motion-compensation-callbacks.md)的支持。 有关详细信息，请参阅 [压缩的视频解码](compressed-video-decoding.md)。

- 如果驱动程序收到 GUID \_ NTCALLBACKS guid，则返回指向 [**DD \_ NTCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_ntcallbacks) 结构的指针。 驱动程序将填充 DD NTCALLBACKS 的成员， \_ 以指示它支持以下回调函数。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">回调函数</th>
  <th align="left">说明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface" data-raw-source="[&lt;em&gt;DdFlipToGDISurface&lt;/em&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface)"><em>DdFlipToGDISurface</em></a></p></td>
  <td align="left"><p>在 DirectDraw 与 GDI 图面翻转时通知驱动程序。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_freedrivermemory" data-raw-source="[&lt;em&gt;DdFreeDriverMemory&lt;/em&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)"><em>DdFreeDriverMemory</em></a></p></td>
  <td align="left"><p>释放屏幕外或非本地显示内存以满足新的分配请求。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><a href="/windows/win32/api/ddrawint/nc-ddrawint-pdd_setexclusivemode" data-raw-source="[&lt;em&gt;DdSetExclusiveMode&lt;/em&gt;](/windows/win32/api/ddrawint/nc-ddrawint-pdd_setexclusivemode)"><em>DdSetExclusiveMode</em></a></p></td>
  <td align="left"><p>DirectDraw 应用程序切换到或从独占模式切换时，通知驱动程序。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   如果驱动程序收到 GUID \_ VIDEOPORTCALLBACKS guid，它将返回指向 [**DD \_ VideoPortCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-dd_videoportcallbacks) 结构的指针，以指示其对 [VPE 回调函数](vpe-callback-functions.md)的支持。 有关详细信息，请参阅 [视频端口扩展到 DirectX](video-port-extensions-to-directx.md)。

