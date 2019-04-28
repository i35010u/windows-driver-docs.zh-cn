---
title: Direct3D 驱动程序初始化
description: Direct3D 驱动程序初始化
ms.assetid: ef37a570-a94e-4021-b84f-4436aa454ac5
keywords:
- 初始化 Direct3D 驱动程序
- Direct3D WDK Windows 2000 显示初始化
- DrvGetDirectDrawInfo
- DdGetDriverInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03cc1294e3bfa84ffd2e3612f52fae24738c857a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342403"
---
# <a name="direct3d-driver-initialization"></a>Direct3D 驱动程序初始化


## <span id="ddk_direct3d_driver_initialization_gg"></span><span id="DDK_DIRECT3D_DRIVER_INITIALIZATION_GG"></span>


当驱动程序的[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229) Microsoft DirectDraw 运行时用于初始化 DirectDraw 支持调用函数，该驱动程序必须执行以下操作来指示其 Microsoft Direct3D功能：

-   设置 DDCAPS\_中的三维标志**ddCaps.dwCaps**的成员[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构，以指示驱动程序的硬件具有 3D加速。

-   设置 DDSCAPS\_*Xxx*标记中**ddCaps.ddsCaps**的 DD 成员\_HALINFO 结构，它描述了 3D 功能的驱动程序的视频内存图面。 下表中列出的标志。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Flag</th>
    <th align="left">含义</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_3DDEVICE</p></td>
    <td align="left"><p>指示作为目标的 3D 渲染，可以使用驱动程序的图面。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>DDSCAPS_TEXTURE</p></td>
    <td align="left"><p>指示可以为 3D 纹理映射使用的驱动程序的图面。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>DDSCAPS_ZBUFFER</p></td>
    <td align="left"><p>指示可以为 Z 缓冲区使用的驱动程序的图面。</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   设置**GetDriverInfo**的成员[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构，以指向驱动程序的[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)回调。 该驱动程序还必须设置 DDHALINFO\_GETDRIVERINFOSET 标志**dwFlags** DD 成员\_HALINFO 结构，以指示它实现了**DdGetDriverInfo**回调。

-   分配并初始化的成员[ **D3DHAL\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff544716)结构，并返回在此结构**lpD3DHALCallbacks** DD 的成员\_HALINFO 结构。

-   分配并初始化的成员[ **D3DHAL\_GLOBALDRIVERDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545963)结构，并返回在此结构**lpD3DGlobalDriverData**成员DD 的\_HALINFO 结构。

若要指示驱动程序是能够使用 Microsoft DirectX 7.0，它应执行以下步骤：

-   包括 D3DDEVCAPS\_DRAWPRIMITIVES2EX 标志**dwDevCaps**的成员[ **D3DDEVICEDESC\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff544689)报告的结构在 Microsoft Direct3D 驱动程序初始化。

-   响应的 GUID\_Miscellaneous2Callbacks GUID **DdGetDriverInfo**通过设置回调**GetDriverState**， **CreateSurfaceEx**，和**DestroyDDLocal**的成员[ **DD\_MISCELLANEOUS2CALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551645)结构。 这些设置为指向 Direct3D 驱动程序和或运算中的相应回调**dwFlags** DDHAL 成员\_MISC2CB32\_CREATESURFACEEX、 DDHAL\_MISC2CB32\_GETDRIVERSTATE 和 DDHAL\_MISC2CB32\_DESTROYDDLOCAL 位，分别。

之后[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)返回，GDI 调用的驱动程序[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)回调几次不同的 Guid若要完成驱动程序的初始化。 **DdGetDriverInfo**回调到支持 Direct3D 的以下 Guid 必须响应：

<span id="GUID_D3DCallbacks3"></span><span id="guid_d3dcallbacks3"></span><span id="GUID_D3DCALLBACKS3"></span>GUID\_D3DCallbacks3  
该驱动程序应分配并初始化的成员[ **D3DHAL\_CALLBACKS3** ](https://msdn.microsoft.com/library/windows/hardware/ff544723)结构，并返回在此结构**lpvData**的成员[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构。

<span id="GUID_Miscellaneous2Callbacks"></span><span id="guid_miscellaneous2callbacks"></span><span id="GUID_MISCELLANEOUS2CALLBACKS"></span>GUID\_Miscellaneous2Callbacks  
该驱动程序应分配并初始化的成员[ **DD\_MISCELLANEOUS2CALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551645)结构，并返回在此结构**lpvData**DD 成员\_GETDRIVERINFODATA 结构。

<span id="GUID_D3DExtendedCaps"></span><span id="guid_d3dextendedcaps"></span><span id="GUID_D3DEXTENDEDCAPS"></span>GUID\_D3DExtendedCaps  
该驱动程序应分配并初始化的适当成员[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)结构，并返回在此结构**lpvData**DD 成员\_GETDRIVERINFODATA 结构。

<span id="GUID_ZPixelFormats"></span><span id="guid_zpixelformats"></span><span id="GUID_ZPIXELFORMATS"></span>GUID\_ZPixelFormats  
该驱动程序应分配并初始化的适当成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)结构的驱动程序支持，并返回这些结构中的每个 Z 缓冲区格式**lpvData** DD 成员\_GETDRIVERINFODATA 结构。 该驱动程序必须响应此 GUID，如果它支持 D3DDP2OP\_在其实现的清除操作代码[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)。

<span id="GUID_D3DParseUnknownCommandCallback"></span><span id="guid_d3dparseunknowncommandcallback"></span><span id="GUID_D3DPARSEUNKNOWNCOMMANDCALLBACK"></span>GUID\_D3DParseUnknownCommandCallback  
该驱动程序应将存储到 Direct3D 运行时的指针**D3DParseUnknownCommand**回调。 将指针传递给驱动程序中**lpvData** DD 成员\_GETDRIVERINFODATA 结构。 在驱动程序[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)回调调用**D3DParseUnknownCommand**回调来分析驱动程序不能识别的命令。

有关详细信息，请参阅[DirectDraw 驱动程序初始化](directdraw-driver-initialization.md)。

 

 





