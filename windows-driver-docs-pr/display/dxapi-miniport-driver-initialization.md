---
title: DxApi 微型端口驱动程序初始化
description: DxApi 微型端口驱动程序初始化
ms.assetid: 8d2bb81c-618e-43e0-9a1a-ff0ceb732d90
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw 初始化
- 初始化 DxApi 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38016e7b0eec98b4d5c0e538ef3f359a0f7b8501
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361221"
---
# <a name="dxapi-miniport-driver-initialization"></a>DxApi 微型端口驱动程序初始化


## <span id="ddk_dxapi_miniport_driver_initialization_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_INITIALIZATION_GG"></span>


若要启用 DxApi 界面功能、 DirectDraw 驱动程序必须在初始化时执行以下任务：

1.  该驱动程序必须指定[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)函数，在[ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构 DirectDraw 可若要获取的其他信息的调用。

2.  *DdGetDriverInfo*回调调用时所使用 GUID\_KernelCallbacks GUID 指定。 该驱动程序必须填写[ **DD\_KERNELCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551633)具有相应的回调和标志一组结构。 该驱动程序然后将复制到此结构**lpvData**的成员[ **DD\_GETDRIVERINFODATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构。

3.  *DdGetDriverInfo*使用的 GUID 调用回调\_KernelCaps GUID 指定。 该驱动程序必须填写[ **DDKERNELCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549593)结构。 该驱动程序然后将复制到此结构**lpvData** DD 成员\_GETDRIVERINFODATA 结构。

4.  DirectDraw 运行时调用的视频端口驱动程序 IOCTL 处理程序替换**MajorFunction** = IRP\_MJ\_PNP， **MinorFunction** = IRP\_MN\_查询\_接口，并**InterfaceType** = GUID\_DxApi。 视频端口驱动程序，然后调用微型端口驱动程序[ *HwVidQueryInterface* ](https://msdn.microsoft.com/library/windows/hardware/ff567358)函数来填充[ **DXAPI\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff557395)使用 DirectDraw 可以调用 DxApi 接口回调函数的指针的结构。 这些回调函数都列在[内核模式视频传输回调函数](kernel-mode-video-transport-callback-functions.md)。

微型端口驱动程序可以指定中的值**上下文**的成员[ **DXAPI\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff557395)传递给微型端口驱动程序的结构这些函数之一的每次调用时。

 

 





