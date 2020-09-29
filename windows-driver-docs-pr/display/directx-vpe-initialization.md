---
title: DirectX VPE 初始化
description: DirectX VPE 初始化
ms.assetid: 1309a302-f9fc-49cf-a6b8-691d0956beab
keywords:
- DirectX VPE 支持 WDK DirectDraw，初始化
- 绘制 VPEs WDK DirectDraw，初始化
- DirectDraw VPEs WDK Windows 2000 显示，初始化
- 视频端口扩展 WDK DirectDraw，初始化
- VPEs WDK DirectDraw，初始化
- 正在初始化 DirectX VPE 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c3ad84c0cda9d4ca038a27f2ebc475186c3322
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423700"
---
# <a name="directx-vpe-initialization"></a>DirectX VPE 初始化


## <span id="ddk_directx_vpe_initialization_gg"></span><span id="DDK_DIRECTX_VPE_INITIALIZATION_GG"></span>


若要启用 VPE 功能，驱动程序必须执行以下操作：

-   调用[**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)时，初始化*pHalInfo*参数所指向的[**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构中嵌入的[**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps)结构的以下成员：
    -   \_在**dwCaps2**中设置 DDCAPS2 VIDEOPORT 标志，以指示显示硬件包含硬件视频端口。 驱动程序还应设置任何其他与硬件相关的 DDCAPS2 \_ *Xxx*标志，以描述设备能够提供的 VPE 支持。
    -   将 **dwMaxVideoPorts** 设置为设备支持的硬件视频端口数。
    -   将 **dwCurrVideoPorts** 初始化为零。
-   在调用 DrvGetDirectDrawInfo 时，实现[**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数并将 DD HALINFO 结构的**GetDriverInfo**成员设置 \_ 为指向此[**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo)函数。 驱动程序的 **DdGetDriverInfo** 函数必须分析 guid \_ VideoPortCallbacks 和 guid \_ VideoPortCaps guid。

-   当使用 GUID VideoPortCallbacks GUID 调用 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 时 \_ ，请使用相应的驱动程序回调和 Flags 集填充 [**DD \_ VideoPortCallbacks**](/windows/win32/api/ddrawint/ns-ddrawint-dd_videoportcallbacks) 结构。 这些回调列在 [VPE 回调函数](vpe-callback-functions.md)中。 然后，该驱动程序必须将此初始化的结构复制到 DirectDraw 分配的缓冲区中，其中[**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构的**lpvData**成员指向该缓冲区，并返回在**dwActualSize**中写入缓冲区的字节数。

-   当用 GUID VideoPortCaps GUID 调用 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) 时 \_ ，请用每个硬件视频端口的功能填写 [**DDVIDEOPORTCAPS**](/windows/win32/api/dvp/ns-dvp-ddvideoportcaps) 结构的数组。 每个硬件视频端口都具有阵列中的一个条目，并且首先指定了硬件视频端口0、下一个指定的硬件视频端口，等等。 如果设备仅支持一个硬件视频端口，数组中将只有一个 DDVIDEOPORTCAPS 结构。 然后，该驱动程序必须将此数据复制到 DirectDraw 分配的缓冲区，其中[**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构的**lpvData**成员指向该缓冲区，并返回在**dwActualSize**中写入缓冲区的字节数。

 

