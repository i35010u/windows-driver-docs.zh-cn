---
title: DirectDraw 和 D3D 回调支持使用 DdGetDriverInfo
description: 显示驱动程序可以实现 DdGetDriverInfo 函数以指示各种 DirectDraw 和 Direct3D 回调支持。
ms.assetid: 7054564e-4520-4900-946a-95c92908667c
keywords:
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示，Windows 2000
- 回调函数 WDK DirectDraw
- DdGetDriverInfo
- Direct3D WDK Windows 2000 显示中回调
- 回调函数 WDK Direct3D
- DirectDraw 驱动程序初始化 WDK Windows 2000 显示中，回调函数
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: a2747373a5496aa32f380000cd5af991f479d611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384858"
---
# <a name="directdraw-and-direct3d-callback-support-using-ddgetdriverinfo"></a>使用 DdGetDriverInfo 的 DirectDraw 和 Direct3D 回调支持

显示驱动程序可以实现[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数以指示各种 DirectDraw 和 Direct3D 回调支持。 回调的支持是取决于驱动程序收到中的以下 Guid **guidInfo**的成员[ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构，向其*lpGetDriverInfo*参数所指向。 该驱动程序中的结构返回指向**lpvData**成员，用于指定 DirectDraw 或 Direct3D 回调支持。

- 如果该驱动程序收到 GUID\_ColorControlCallbacks GUID，它将返回一个指向[ **DD\_COLORCONTROLCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks)结构。 如果它支持[颜色控制](color-control-initialization.md)，驱动程序填充**ColorControl** DD 成员\_COLORCONTROLCALLBACKS 指定其[ *DdControlColor*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol)回调函数。

- 如果该驱动程序收到 GUID\_D3DCallbacks，GUID\_D3DCallbacks3 或 GUID\_Miscellaneous2Callbacks GUID，它将返回一个指向[ **D3DHAL\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks)， [ **D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_callbacks3)，或者[ **DD\_MISCELLANEOUS2CALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)结构。 驱动程序使用这些结构指示其[Direct3D 回调支持](driver-functions-to-support-direct3d.md)。 有关详细信息，请参阅[Direct3D DDI](direct3d.md)。

- 如果该驱动程序收到 GUID\_KernelCallbacks GUID，它将返回一个指向[ **DD\_KERNELCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)结构。 该驱动程序填充的 DD 成员\_KERNELCALLBACKS 以指示它支持以下的回调函数。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">回调函数</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface" data-raw-source="[&lt;em&gt;DdSyncSurfaceData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncsurface)"><em>DdSyncSurfaceData</em></a></p></td>
  <td align="left"><p>设置并修改图面上的数据。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport" data-raw-source="[&lt;em&gt;DdSyncVideoPortData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)"><em>DdSyncVideoPortData</em></a></p></td>
  <td align="left"><p>设置并修改的视频端口扩展 (VPE) 对象的数据。</p></td>
  </tr>
  </tbody>
  </table>

- 如果该驱动程序收到 GUID\_MiscellaneousCallbacks GUID，它将返回一个指向[ **DD\_MISCELLANEOUSCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneouscallbacks)结构。 如果它支持[ *DdGetAvailDriverMemory* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory)回调函数、 驱动程序填充*DdGetAvailDriverMemory*的 DD 成员\_若要指定 MISCELLANEOUSCALLBACKS *DdGetAvailDriverMemory*。

- 如果该驱动程序收到 GUID\_MotionCompCallbacks GUID，它将返回一个指向[ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构，以指示其支持[动作补偿回调](motion-compensation-callbacks.md)。 有关详细信息，请参阅[压缩视频解码](compressed-video-decoding.md)。

- 如果该驱动程序收到 GUID\_NTCallbacks GUID，它将返回一个指向[ **DD\_NTCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_ntcallbacks)结构。 该驱动程序填充的 DD 成员\_NTCALLBACKS 以指示它支持以下的回调函数。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">回调函数</th>
  <th align="left">描述</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface" data-raw-source="[&lt;em&gt;DdFlipToGDISurface&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_fliptogdisurface)"><em>DdFlipToGDISurface</em></a></p></td>
  <td align="left"><p>DirectDraw 翻转到或从 GDI 图面时，会通知驱动程序。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory" data-raw-source="[&lt;em&gt;DdFreeDriverMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)"><em>DdFreeDriverMemory</em></a></p></td>
  <td align="left"><p>释放屏幕外或非本地显示内存以满足新的分配请求。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode" data-raw-source="[&lt;em&gt;DdSetExclusiveMode&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode)"><em>DdSetExclusiveMode</em></a></p></td>
  <td align="left"><p>DirectDraw 应用程序切换到或从独占模式时，会通知驱动程序。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   如果该驱动程序收到 GUID\_VideoPortCallbacks GUID，它将返回一个指向[ **DD\_VIDEOPORTCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_videoportcallbacks)结构，以指示其支持[VPE 回调函数](vpe-callback-functions.md)。 有关详细信息，请参阅[DirectX 的视频端口扩展](video-port-extensions-to-directx.md)。

 

 





