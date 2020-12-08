---
title: 初始化 D3D User-Mode 显示驱动程序通信
description: 初始化与 Direct3D 用户模式显示驱动程序之间的通信
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，初始化
- Direct3D WDK 显示
- 用户模式显示驱动程序 WDK Windows Vista，Direct3D
ms.date: 09/17/2019
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 9c7967d98685a477ed63157c88a99d9759a7974b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827261"
---
# <a name="initializing-communication-with-the-direct3d-user-mode-display-driver"></a>初始化与 Direct3D 用户模式显示驱动程序之间的通信

若要初始化与 Microsoft Direct3D 用户模式显示驱动程序 DLL 的版本 11 DDI 的通信，Direct3D 运行时首先加载 DLL。 接下来，Direct3D 运行时通过 DLL 的导出表调用用户模式显示驱动程序的 [**OpenAdapter**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter) 函数，以打开图形适配器的实例。 *OpenAdapter* 函数是 DLL 的唯一导出函数。

在对驱动程序的 *OpenAdapter* 函数的调用中，运行时在 [**D3DDDIARG \_ OpenAdapter**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_openadapter)结构的 **pAdapterCallbacks** 成员中提供 [**pfnQueryAdapterInfoCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)适配器回调函数。 运行时还会在 D3DDDIARG OPENADAPTER 的 **接口** 和 **版本** 成员中提供其版本 \_ 。 用户模式显示驱动程序必须验证它是否可以使用此版本的运行时。 用户模式显示驱动程序返回 D3DDDIARG_OPENADAPTER 的 **pAdapterFuncs** 成员中其特定于适配器的函数的表。

用户模式显示驱动程序应调用 [**pfnQueryAdapterInfoCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb) 适配器回调函数以从显示微型端口驱动程序查询图形硬件功能。

运行时调用用户模式显示驱动程序的 [**CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice) 函数 (某个驱动程序的适配器特定函数) 创建显示设备，用于处理渲染状态的集合和完成初始化。 初始化完成后，Direct3D 运行时可以调用 [显示器驱动程序提供的函数](/windows-hardware/drivers/ddi/index)，用户模式显示驱动程序可以调用 [运行时提供的函数](/windows-hardware/drivers/ddi/index)。

用户模式显示驱动程序的 *CreateDevice* 函数使用 [**D3DDDIARG \_ CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createdevice) 结构调用，该结构的成员按以下方式设置以初始化用户模式显示驱动程序接口：

- 运行时将 **接口** 设置为运行时需要用户模式显示驱动程序的接口版本。

- 运行时将 **版本** 设置为一个数字，驱动程序可以使用该数字来确定运行时的生成时间。 例如，驱动程序可以使用版本号来区分与 Windows Vista 一起发布的运行时，并使用后续 Service Pack 发布的运行时，其中可能包含驱动程序所需的修补程序。

- 运行时设置 **hDevice** ，以指定驱动程序回调到运行时时应使用的句柄。 驱动程序生成一个唯一的句柄，并将其传递回 **hDevice** 中的运行时。 运行时应在后续的驱动程序调用中使用返回的 **hDevice** 句柄。

- 运行时在 [**D3DDDI_DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks) 结构中提供其特定于设备的回调函数的表， **pCallbacks** 点。 用户模式显示驱动程序调用运行时提供的回调函数，以访问显示微型端口驱动程序中的内核模式服务。

- 用户模式显示驱动程序会将其设备特定函数的表返回到 **pDeviceFuncs** 点的 [**D3DDDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)结构中。

> [!NOTE]
>  (图形上下文) 可以同时存在的显示设备的数量仅受可用系统内存限制。
