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
ms.openlocfilehash: 7f546f5e74def26fb93afeffd88d213120eda6ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839000"
---
# <a name="directdraw-and-direct3d-callback-support-using-ddgetdriverinfo"></a>使用 DdGetDriverInfo 的 DirectDraw 和 Direct3D 回调支持

显示驱动程序可以实现[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数，以指示各种 DirectDraw 和 Direct3D 回调支持。 回调支持是由驱动程序在[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**guidInfo**成员中接收到的、 *LpGetDriverInfo*参数所指向的 guid。 驱动程序返回指向**lpvData**成员中的结构的指针，该结构指定 DirectDraw 或 Direct3D 回叫支持。

- 如果驱动程序收到 GUID\_ColorControlCallbacks GUID，则返回指向[**DD\_ColorControlCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_colorcontrolcallbacks)结构的指针。 如果支持[颜色控制](color-control-initialization.md)，驱动程序将填充 DD\_COLORCONTROLCALLBACKS 的**ColorControl**成员，以指定其[*DdControlColor*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_colorcb_colorcontrol)回调函数。

- 如果驱动程序收到 GUID\_D3DCallbacks、GUID\_D3DCallbacks3 或 GUID\_Miscellaneous2Callbacks GUID，它将返回指向[**D3DHAL\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks)、 [**D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks3)或 DD 的指针[ **\_MISCELLANEOUS2CALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)结构。 驱动程序使用这些结构来指示其[Direct3D 回叫支持](driver-functions-to-support-direct3d.md)。 有关详细信息，请参阅[DIRECT3D DDI](direct3d.md)。

- 如果驱动程序收到 GUID\_KernelCallbacks GUID，则返回指向[**DD\_KernelCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)结构的指针。 驱动程序将填充 DD\_KERNELCALLBACKS 的成员，以指示它支持以下回调函数。

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
  <td align="left"><p>设置和修改表面数据。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport" data-raw-source="[&lt;em&gt;DdSyncVideoPortData&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_kernelcb_syncvideoport)"><em>DdSyncVideoPortData</em></a></p></td>
  <td align="left"><p>设置和修改视频端口扩展（VPE）对象数据。</p></td>
  </tr>
  </tbody>
  </table>

- 如果驱动程序收到 GUID\_MiscellaneousCallbacks GUID，则返回指向[**DD\_MiscellaneousCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneouscallbacks)结构的指针。 如果它支持[*DdGetAvailDriverMemory*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory)回调函数，则驱动程序将填充 DD\_MISCELLANEOUSCALLBACKS 的*DdGetAvailDriverMemory*成员来指定*DdGetAvailDriverMemory*。

- 如果驱动程序收到 GUID\_MotionCompCallbacks GUID，它将返回一个指向[**DD\_MotionCompCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的指针，以指示其对[运动补偿回调](motion-compensation-callbacks.md)的支持。 有关详细信息，请参阅[压缩的视频解码](compressed-video-decoding.md)。

- 如果驱动程序收到 GUID\_NTCallbacks GUID，则返回指向[**DD\_NTCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_ntcallbacks)结构的指针。 驱动程序将填充 DD\_NTCALLBACKS 的成员，以指示它支持以下回调函数。

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
  <td align="left"><p>在 DirectDraw 与 GDI 图面翻转时通知驱动程序。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory" data-raw-source="[&lt;em&gt;DdFreeDriverMemory&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_freedrivermemory)"><em>DdFreeDriverMemory</em></a></p></td>
  <td align="left"><p>释放屏幕外或非本地显示内存以满足新的分配请求。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode" data-raw-source="[&lt;em&gt;DdSetExclusiveMode&lt;/em&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_setexclusivemode)"><em>DdSetExclusiveMode</em></a></p></td>
  <td align="left"><p>DirectDraw 应用程序切换到或从独占模式切换时，通知驱动程序。</p></td>
  </tr>
  </tbody>
  </table>

     

<!-- -->

-   如果驱动程序收到 GUID\_VideoPortCallbacks GUID，它将返回一个指向[**DD\_VideoPortCallbacks**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_videoportcallbacks)结构的指针，以指示其对[VPE 回调函数](vpe-callback-functions.md)的支持。 有关详细信息，请参阅[视频端口扩展到 DirectX](video-port-extensions-to-directx.md)。

 

 





