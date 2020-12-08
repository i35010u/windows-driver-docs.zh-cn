---
title: DxApi 微型端口驱动程序初始化
description: DxApi 微型端口驱动程序初始化
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw，初始化
- 正在初始化 DxApi 微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ba3b3c79f4988ee4953786666bf00c7d61839c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809081"
---
# <a name="dxapi-miniport-driver-initialization"></a>DxApi 微型端口驱动程序初始化


## <span id="ddk_dxapi_miniport_driver_initialization_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_INITIALIZATION_GG"></span>


若要启用 DxApi 接口功能，DirectDraw 驱动程序必须在初始化时执行以下任务：

1.  驱动程序必须在 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构中指定 [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)函数，而 DirectDraw 可以调用该函数以获取其他信息。

2.  用指定的 GUID KernelCallbacks GUID 调用 *DdGetDriverInfo* 回调 \_ 。 驱动程序必须在 [**DD \_ KERNELCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_kernelcallbacks) 结构中填写适当的回调和标志集。 然后，该驱动程序将此结构复制到 [**DD \_ GETDRIVERINFODATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_getdriverinfodata)结构的 **lpvData** 成员。

3.  在指定 GUID KernelCaps GUID 的情况调用 *DdGetDriverInfo* 回调 \_ 。 驱动程序必须填写 [**DDKERNELCAPS**](/windows/win32/api/ddkernel/ns-ddkernel-ddkernelcaps) 结构。 然后，该驱动程序将此结构复制到 DD GETDRIVERINFODATA 结构的 **lpvData** 成员 \_ 。

4.  DirectDraw 运行时调用视频端口驱动程序 IOCTL 处理程序，其 **MajorFunction** = irp \_ MJ \_ PNP， **MinorFunction** = irp \_ MN \_ 查询 \_ 接口， **InterfaceType** = GUID \_ DxApi。 然后，视频端口驱动程序调用视频微型端口驱动程序的 [*HwVidQueryInterface*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface) 函数，以便在 [**DXAPI \_ 接口**](/windows/win32/api/dxmini/ns-dxmini-dxapi_interface) 结构中填充 DirectDraw 可以调用的 DXAPI 接口回调函数的指针。 [内核模式视频传输回调函数](kernel-mode-video-transport-callback-functions.md)中列出了这些回调函数。

在每次调用其中一个函数时，视频微型端口驱动程序都可以在 [**DXAPI \_ 接口**](/windows/win32/api/dxmini/ns-dxmini-dxapi_interface)结构的 **上下文** 成员中指定一个值。

 

