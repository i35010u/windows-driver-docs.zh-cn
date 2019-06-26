---
title: 初始化与 Direct3D 版本 10 DDI 之间的通信
description: 初始化与 Direct3D 版本 10 DDI 之间的通信
ms.assetid: dc3cc26f-7295-46d6-9bd7-aae7027ea92c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf86cbea15bd7e5e182a64a5b7da76195ec82694
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385188"
---
# <a name="initializing-communication-with-the-direct3d-version-10-ddi"></a>初始化与 Direct3D 版本 10 DDI 之间的通信


初始化与用户模式显示驱动程序 DLL 版本之间的通信 10 DDI 的 Direct3D 版本 10 运行时首次加载该 DLL 如果尚未加载该 DLL。 Direct3D 运行时接下来将调用用户模式显示驱动程序[ **OpenAdapter10** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数通过 DLL 的导出表以打开图形适配器的实例。 *OpenAdapter10*函数仅用于 DLL 的导出的 Direct3D 版本 10 函数。

对驱动程序的调用中*OpenAdapter10*函数，运行时会提供[ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)适配器中的回调函数**pAdapterCallbacks**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构。 运行时还提供在其版本号**接口**并**版本**D3D10DDIARG 成员\_OPENADAPTER。 用户模式显示驱动程序必须验证，它可以使用此版本的运行时。 由于较新的运行时版本可以使用 DDI 旧版并因此可以正确地与之通信实现这些旧 DDI 版本的驱动程序，因此，用户模式显示驱动程序必须故障的运行时的较新版本。 用户模式显示驱动程序将返回一个表中其特定于适配器的函数**pAdapterFuncs** D3D10DDIARG 成员\_OPENADAPTER。

用户模式显示驱动程序应调用[ **pfnQueryAdapterInfoCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)适配器回调函数来查询的图形硬件功能中的显示微型端口驱动程序。

运行时调用用户模式显示驱动程序[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数 （驱动程序的特定于适配器的功能之一） 创建用于处理的呈现状态集合的显示设备并完成初始化。 初始化完成后，可以调用 Direct3D 版本 10 运行时[显示驱动程序提供的 Direct3D 版本 10 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，并且用户模式显示驱动程序可以调用[运行时提供的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index).

用户模式显示驱动程序*CreateDevice(D3D10)* 使用调用函数[ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)中设置其成员的结构通过以下方式来初始化用户模式显示驱动程序的版本 10 DDI:

-   运行时设置**接口**到运行时需要从用户模式显示驱动程序接口的版本。

-   运行时设置**版本**驱动程序可用于标识时，运行时生成的数字。 例如，驱动程序可以使用的版本号随 Windows Vista 一起发布的运行时和后续的 service pack，其中可能包含驱动程序需要的修补程序发布的运行时之间进行区分。

-   运行时设置**hRTDevice**来指定当驱动程序回调到运行时，应使用该驱动程序的句柄。

-   运行时设置**hDrvDevice**在后续的驱动程序调用中指定运行时使用的句柄。

-   运行时会提供在其设备特定的回调函数的表[ **D3DDDI\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)向其结构**pKTCallbacks**点. 用户模式显示驱动程序调用访问显示微型端口驱动程序中的内核模式服务的运行时提供的回调函数。

-   用户模式显示驱动程序将返回一个表中其特定于设备的函数[ **D3D10DDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)向其结构**pDeviceFuncs**点。

-   运行时会提供[ **DXGI\_DDI\_基本\_ARGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)向其结构**DXGIBaseDDI**点。 在运行时和用户模式显示驱动程序提供其[DirectX 图形基础结构 DDI](directx-graphics-infrastructure-ddi.md)此结构。

-   运行时设置**hRTCoreLayer**以指定驱动程序时驱动程序回调到访问核心 Direct3D 10 功能的运行时应使用的句柄 (即，在调用函数的**pUMCallbacks**成员指定)。

-   运行时会提供在其核心回调函数的表[ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构到**pUMCallbacks**点。 用户模式显示驱动程序调用运行时提供核心回调函数来刷新状态。

**请注意**  显示设备 （图形上下文中） 可以同时存在数仅受可用系统内存。

 

 

 





