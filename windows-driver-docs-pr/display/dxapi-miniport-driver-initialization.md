---
title: DxApi 微型端口驱动程序初始化
description: DxApi 微型端口驱动程序初始化
ms.assetid: 8d2bb81c-618e-43e0-9a1a-ff0ceb732d90
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw，初始化
- 正在初始化 DxApi 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025d92491472b598a176840d226f6cf58883f2e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838976"
---
# <a name="dxapi-miniport-driver-initialization"></a>DxApi 微型端口驱动程序初始化


## <span id="ddk_dxapi_miniport_driver_initialization_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_INITIALIZATION_GG"></span>


若要启用 DxApi 接口功能，DirectDraw 驱动程序必须在初始化时执行以下任务：

1.  驱动程序必须\_在[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数中指定[**HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构，DirectDraw 可以调用该函数以获取其他信息。

2.  *DdGetDriverInfo*回调是通过指定 Guid\_KernelCallbacks guid 来调用的。 驱动程序必须在[**DD\_KERNELCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_kernelcallbacks)结构中填写适当的回调和标志集。 然后，该驱动程序将此结构复制到[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)结构的**lpvData**成员。

3.  *DdGetDriverInfo*回调是通过指定 Guid\_KernelCaps guid 来调用的。 驱动程序必须填写[**DDKERNELCAPS**](https://docs.microsoft.com/windows/desktop/api/ddkernel/ns-ddkernel-_ddkernelcaps)结构。 然后，该驱动程序将此结构复制到 DD\_GETDRIVERINFODATA 结构的**lpvData**成员。

4.  DirectDraw 运行时调用视频端口驱动程序 IOCTL 处理程序，其中**MajorFunction** = IRP\_MJ\_PNP， **MinorFunction** = IRP\_MN\_查询\_接口， **InterfaceType** = GUID\_DxApi。 然后，视频端口驱动程序调用视频微型端口驱动程序的[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)函数，以填充[**DXAPI\_接口**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)结构，该结构包含指向 DirectDraw 可以调用的 DXAPI 接口回调函数的指针。 [内核模式视频传输回调函数](kernel-mode-video-transport-callback-functions.md)中列出了这些回调函数。

在每次调用其中一个函数时，视频微型端口驱动程序都可以在[**DXAPI\_接口**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)结构的**上下文**成员中指定一个值。

 

 





