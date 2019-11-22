---
title: Direct3D 驱动程序初始化
description: Direct3D 驱动程序初始化
ms.assetid: ef37a570-a94e-4021-b84f-4436aa454ac5
keywords:
- 正在初始化 Direct3D 驱动程序
- Direct3D WDK Windows 2000 显示，初始化
- DrvGetDirectDrawInfo
- DdGetDriverInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebfaa21273c0d73df8ba8bbe50d264e639ae0948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839012"
---
# <a name="direct3d-driver-initialization"></a>Direct3D 驱动程序初始化


## <span id="ddk_direct3d_driver_initialization_gg"></span><span id="DDK_DIRECT3D_DRIVER_INITIALIZATION_GG"></span>


当 Microsoft DirectDraw 运行时调用驱动程序的[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)函数以初始化 DirectDraw 支持时，驱动程序必须执行以下操作来指示其 Microsoft Direct3D 功能：

-   在[**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**dwCaps**成员中设置 DDCAPS\_3d 标志，以指示驱动程序的硬件具有3d 加速功能。

-   在描述驱动程序视频内存图的三维功能的 DD\_HALINFO 结构的 ddsCaps 成员中设置 DDSCAPS\_*Xxx*标志 **。** 下表列出了这些标志。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">旗帜</th>
    <th align="left">含义</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_3DDEVICE</p></td>
    <td align="left"><p>指示驱动程序的图面可用作三维呈现的目标。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDSCAPS_TEXTURE</p></td>
    <td align="left"><p>指示驱动程序的图面可以用于3D 纹理映射。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_ZBUFFER</p></td>
    <td align="left"><p>指示驱动程序的图面可用作 Z 缓冲区。</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   将[**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**GetDriverInfo**成员设置为指向驱动程序的[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)回调。 驱动程序还必须在 DD\_HALINFO 结构的**dwFlags**成员中设置 DDHALINFO\_GETDRIVERINFOSET 标志，以指示它已实现**DdGetDriverInfo**回调。

-   分配并初始化[**D3DHAL\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks)结构的成员，并在 DD\_HALINFO 结构的**lpD3DHALCallbacks**成员中返回此结构。

-   分配并初始化[**D3DHAL\_GLOBALDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)结构的成员，并在 DD\_HALINFO 结构的**lpD3DGlobalDriverData**成员中返回此结构。

若要指示驱动程序可以使用 Microsoft DirectX 7.0，应执行以下操作：

-   将 D3DDEVCAPS\_DRAWPRIMITIVES2EX 标志包含在 Microsoft Direct3D 驱动程序初始化过程中报告的[**D3DDEVICEDESC\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3ddevicedesc_v1)结构的**dwDevCaps**成员中。

-   通过设置[**DD\_DestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)结构的**GetDriverState**、 **CreateSurfaceEx**和**Miscellaneous2Callbacks**成员来响应**DdGetDriverInfo**回调中的 guid\_Miscellaneous2Callbacks guid。 这些设置为指向**dwFlags**成员中 Direct3D 驱动程序和运算的适当回调，其中包含 DDHAL\_MISC2CB32\_CREATESURFACEEX、DDHAL\_MISC2CB32\_GETDRIVERSTATE 和 DDHAL\_MISC2CB32分别\_DESTROYDDLOCAL 位。

[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)返回后，GDI 将为不同的 guid 调用驱动程序的[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)回调若干次，以完成驱动程序的初始化。 **DdGetDriverInfo**回调必须响应以下 guid 以支持 Direct3D：

<span id="GUID_D3DCallbacks3"></span><span id="guid_d3dcallbacks3"></span><span id="GUID_D3DCALLBACKS3"></span>GUID\_D3DCallbacks3  
驱动程序应分配并初始化[**D3DHAL\_CALLBACKS3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_callbacks3)结构的成员，并在[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**lpvData**成员中返回此结构。

<span id="GUID_Miscellaneous2Callbacks"></span><span id="guid_miscellaneous2callbacks"></span><span id="GUID_MISCELLANEOUS2CALLBACKS"></span>GUID\_Miscellaneous2Callbacks  
驱动程序应分配并初始化[**dd\_MISCELLANEOUS2CALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_miscellaneous2callbacks)结构的成员，并在 DD\_GETDRIVERINFODATA 结构的**lpvData**成员中返回此结构。

<span id="GUID_D3DExtendedCaps"></span><span id="guid_d3dextendedcaps"></span><span id="GUID_D3DEXTENDEDCAPS"></span>GUID\_D3DExtendedCaps  
驱动程序应分配并初始化[**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)结构的相应成员，并在 DD\_GETDRIVERINFODATA 结构的**lpvData**成员中返回此结构。

<span id="GUID_ZPixelFormats"></span><span id="guid_zpixelformats"></span><span id="GUID_ZPIXELFORMATS"></span>GUID\_ZPixelFormats  
驱动程序应为驱动程序支持的每个 Z 缓冲区格式分配和初始化[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的相应成员，并将这些结构返回到 DD 的**LPVDATA**成员\_GETDRIVERINFODATA构造. 如果驱动程序支持 D3DDP2OP 在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)的实现中\_清除操作代码，则必须响应此 GUID。

<span id="GUID_D3DParseUnknownCommandCallback"></span><span id="guid_d3dparseunknowncommandcallback"></span><span id="GUID_D3DPARSEUNKNOWNCOMMANDCALLBACK"></span>GUID\_D3DParseUnknownCommandCallback  
驱动程序应将指针存储到 Direct3D 运行时的**D3DParseUnknownCommand**回调。 将指针传递到 DD\_GETDRIVERINFODATA 结构的**lpvData**成员中的驱动程序。 驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调调用**D3DParseUnknownCommand**回调来解析驱动程序无法识别的命令。

有关详细信息，请参阅[DirectDraw 驱动程序初始化](directdraw-driver-initialization.md)。

 

 





