---
title: 初始化与 Direct3D 版本 10 DDI 之间的通信
description: 初始化与 Direct3D 版本 10 DDI 之间的通信
ms.assetid: dc3cc26f-7295-46d6-9bd7-aae7027ea92c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f0dc0d7d1e8d203b9bf3c38dc9c9cd33c658018
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067418"
---
# <a name="initializing-communication-with-the-direct3d-version-10-ddi"></a>初始化与 Direct3D 版本 10 DDI 之间的通信


若要初始化与用户模式显示驱动程序 DLL 的版本 10 DDI 的通信，Direct3D 版本10运行时首先会加载 DLL （如果尚未加载 DLL）。 接下来，Direct3D 运行时通过 DLL 的导出表调用用户模式显示驱动程序的 [**OpenAdapter10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) 函数，以打开图形适配器的实例。 *OpenAdapter10*函数是 DLL 的唯一导出 Direct3D 版本10函数。

在对驱动程序的*OpenAdapter10*函数的调用中，运行时在[**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的**pAdapterCallbacks**成员中提供[**pfnQueryAdapterInfoCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)适配器回调函数。 运行时还会在 D3D10DDIARG OPENADAPTER 的 **接口** 和 **版本** 成员中提供其版本 \_ 。 用户模式显示驱动程序必须验证它是否可以使用此版本的运行时。 用户模式显示驱动程序不得导致更新版本的运行时失败，因为较新的运行时版本可以使用以前的 DDI 版本，因此可以正确地与实现以前的 DDI 版本的驱动程序通信。 用户模式显示驱动程序返回 D3D10DDIARG OPENADAPTER 的 **pAdapterFuncs** 成员中其适配器特定函数的表 \_ 。

用户模式显示驱动程序应调用 [**pfnQueryAdapterInfoCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) 适配器回调函数以从显示微型端口驱动程序查询图形硬件功能。

运行时调用用户模式显示驱动程序的 [**CreateDevice (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice) 函数 (某个驱动程序的适配器特定函数) 来创建显示设备，用于处理呈现状态的集合并完成初始化。 初始化完成后，Direct3D 版本10运行时可以调用 [显示器驱动程序提供的 Direct3D 版本10函数](/windows-hardware/drivers/ddi/index)，并且用户模式显示驱动程序可以调用 [运行时提供的函数](/windows-hardware/drivers/ddi/index)。

用户模式显示驱动程序的 *CreateDevice (D3D10) * 函数使用一个 [**D3D10DDIARG \_ CreateDevice**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice) 结构调用，该结构的成员按以下方式设置，以初始化用户模式显示驱动程序的第10版 DDI：

-   运行时将 **接口** 设置为运行时需要用户模式显示驱动程序的接口版本。

-   运行时将 **版本** 设置为一个数字，驱动程序可以使用该数字来确定运行时的生成时间。 例如，驱动程序可以使用版本号来区分与 Windows Vista 一起发布的运行时，并使用后续 Service Pack 发布的运行时，其中可能包含驱动程序所需的修补程序。

-   运行时设置 **hRTDevice** ，以指定驱动程序回调到运行时时应使用的句柄。

-   运行时设置 **hDrvDevice** 以指定运行时在后续的驱动程序调用中使用的句柄。

-   运行时在**pKTCallbacks**点的[**D3DDDI \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)结构中提供其特定于设备的回调函数的表。 用户模式显示驱动程序调用运行时提供的回调函数，以访问显示微型端口驱动程序中的内核模式服务。

-   用户模式显示驱动程序会将其设备特定函数的表返回到**pDeviceFuncs**点的[**D3D10DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_devicefuncs)结构中。

-   运行时提供一个**DXGIBaseDDI**点的[**DXGI \_ DDI \_ 基 \_ 参数**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)结构。 运行时和用户模式显示驱动程序将其 [DirectX 图形基础结构](directx-graphics-infrastructure-ddi.md) 提供到此结构中。

-   运行时将设置 **hRTCoreLayer** ，以指定当驱动程序回叫运行时以访问 core Direct3D 10 功能时，驱动程序应使用的句柄， (即，调用 **pUMCallbacks** 成员指定的函数) 。

-   运行时在**pUMCallbacks**指向的[**D3D10DDI \_ CORELAYER \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构中提供其核心回调函数的表。 用户模式显示驱动程序调用运行时提供的核心回调函数以刷新状态。

**注意**   可以同时存在 (图形上下文) 的显示设备数仅受可用系统内存限制。

 

 

