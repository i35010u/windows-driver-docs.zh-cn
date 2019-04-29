---
title: DirectX VPE 初始化
description: DirectX VPE 初始化
ms.assetid: 1309a302-f9fc-49cf-a6b8-691d0956beab
keywords:
- DirectX VPE 支持 WDK DirectDraw、 初始化
- 绘制 VPEs WDK DirectDraw 初始化
- DirectDraw VPEs WDK Windows 2000 显示初始化
- 视频端口扩展 WDK DirectDraw、 初始化
- VPEs WDK DirectDraw 初始化
- 初始化 DirectX VPE 功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e48e0fb05bf84a41470e900d02ea8af473fc45ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392040"
---
# <a name="directx-vpe-initialization"></a>DirectX VPE 初始化


## <span id="ddk_directx_vpe_initialization_gg"></span><span id="DDK_DIRECTX_VPE_INITIALIZATION_GG"></span>


若要启用 VPE 功能，该驱动程序必须执行以下操作：

-   当[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)是调用，初始化的以下成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248) 中嵌入的结构[**DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)向其结构*pHalInfo*参数所指向：
    -   设置 DDCAPS2\_中的视频端口标志**dwCaps2**以指示显示硬件包含硬件的视频端口。 该驱动程序还应设置任何其他硬件视频端口相关 DDCAPS2\_*Xxx*标志来描述 VPE 支持是否支持的设备。
    -   设置**dwMaxVideoPorts**到硬件设备支持的视频端口数。
    -   初始化**dwCurrVideoPorts**为零。
-   实现[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)函数，并设置**GetDriverInfo**的 DD 成员\_HALINFO 结构以指向此函数时[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)调用。 在驱动程序**DdGetDriverInfo**函数必须分析 GUID\_VideoPortCallbacks 和 GUID\_VideoPortCaps Guid。

-   当[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)调用使用 GUID\_VideoPortCallbacks GUID 填写[ **DD\_VIDEOPORTCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551758)与相应的驱动程序回调和标记集的结构。 中列出了这些回调[VPE 回调函数](vpe-callback-functions.md)。 驱动程序必须随后将此初始化的结构复制到 DirectDraw 分配缓冲区所属**lpvData**的成员[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构，点，并返回到缓冲区中写入的字节数**dwActualSize**。

-   当[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)调用使用 GUID\_VideoPortCaps GUID 的数组中填充[ **DDVIDEOPORTCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550376)与每个硬件的视频端口的功能的结构。 每个硬件的视频端口有一个条目在数组中，与硬件零的视频端口首先，指定硬件的视频端口指定接下来，依次类推。 如果设备支持只有一个硬件视频端口，将仅有一个 DDVIDEOPORTCAPS 结构数组中。 该驱动程序必须随后将此数据复制到 DirectDraw 分配到的缓冲区**lpvData**的成员[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构点，并返回到缓冲区中写入的字节数**dwActualSize**。

 

 





