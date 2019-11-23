---
title: 初始化与 Direct3D 版本 11 DDI 之间的通信
description: 初始化与 Direct3D 版本 11 DDI 之间的通信
ms.assetid: 3b383f78-da88-4979-b55f-8e234f230df7
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，初始化 DDI 通信
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，初始化 DDI 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a08d666739d8daee6028b5055d1f21edda80c10
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840371"
---
# <a name="initializing-communication-with-the-direct3d-version-11-ddi"></a>初始化与 Direct3D 版本 11 DDI 之间的通信


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

若要初始化与用户模式显示驱动程序 DLL 的版本 11 DDI 的通信，Direct3D 版本11运行时首先会加载 dll （如果尚未加载 DLL）。 然后，Direct3D 运行时通过 DLL 的导出表调用用户模式显示驱动程序的[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数，以打开图形适配器的实例。 **OpenAdapter10\_2**函数是 DLL 的唯一导出函数。

**请注意**   [**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数与[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数相同，不同之处在于**OpenAdapter10\_2**在[**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的**pAdapterFuncs\_2**成员中返回驱动程序的适配器特定函数的表， **OpenAdapter10**返回 pAdapterFuncs\_D3D10DDIARG 的 OPENADAPTER 成员的驱动程序适配器特定函数的表。 **pAdapterFuncs\_2**指向[**D3D10\_2DDI\_ADAPTERFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构;**pAdapterFuncs**指向[**D3D10DDI\_ADAPTERFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_adapterfuncs)结构。

 

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)旨在提高初始化驱动程序的效率。 必须在 Direct3D 版本11驱动程序中实现**OpenAdapter10\_2** 。 你还可以在 Direct3D 版本10.1 驱动程序中实现**OpenAdapter10\_2** （而不是[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)），以提高这些驱动程序的初始化效率。 有关在 Direct3D 版本10.1 驱动程序中实现**OpenAdapter10\_2**的详细信息，请参阅[版本发现支持](version-discovery-support.md)。 **OpenAdapter10\_2**用于处理运行时和驱动程序之间的版本控制和其他信息。

### <a name="span-idversioningspanspan-idversioningspanversioning"></a><span id="versioning"></span><span id="VERSIONING"></span>控制

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)和驱动程序的适配器特定的函数会更改 direct3d API 和 direct3d DDI 之间的版本控制的处理方式是从 direct3d 10 处理版本控制的方式进行处理（有关 direct3d 10 如何处理版本控制的详细信息，请参阅[初始化与 direct3d 版本10的通信](initializing-communication-with-the-direct3d-version-10-ddi.md)）。 该驱动程序必须显式列出它支持的 DDI 版本，而不是依赖于驱动程序的 OpenAdapter10 的失败，而不是依赖于驱动程序的 **\_2**函数来指示不支持特定版本（与**OpenAdapter10\_2**） Direct3D 运行时调用用户模式显示驱动程序的[**GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)函数（驱动程序的适配器特定的一个函数）来查询驱动程序支持的 DDI 版本。

至少有两个新的 DDI 版本适用于 Direct3D 11 DDI 函数。 每个 DDI 版本都区分 DDI 是否在 Windows Vista 或 Windows 7 上运行。 但是，支持 Direct3D 11 DDI 并不一定表示完全支持与 D3D\_功能\_级别\_11 关联的硬件功能。 驱动程序可以支持 Direct3D 11 DDI 的新线程功能，其中的硬件不支持 Direct3D 11 DDI （如镶嵌等）公开的其他功能。 下面的代码演示了每个 DDI 版本之间的区别：

```cpp
// D3D11.0 on Vista
#define D3D11_DDI_MAJOR_VERSION 11
#define D3D11_0_DDI_MINOR_VERSION ...
#define D3D11_0_DDI_INTERFACE_VERSION \
    ((D3D11_DDI_MAJOR_VERSION << 16) | D3D11_0_DDI_MINOR_VERSION)
#define D3D11_0_DDI_BUILD_VERSION ...
#define D3D11_0_DDI_SUPPORTED \
    ((((UINT64)D3D11_0_DDI_INTERFACE_VERSION) << 32) | \
    (((UINT64)D3D11_0_DDI_BUILD_VERSION) << 16))

// D3D11.0 on Windows 7
#define D3D11_0_7_DDI_MINOR_VERSION ...
#define D3D11_0_7_DDI_INTERFACE_VERSION \
    ((D3D11_DDI_MAJOR_VERSION << 16) | D3D11_0_7_DDI_MINOR_VERSION)
#define D3D11_0_7_DDI_BUILD_VERSION ...
#define D3D11_0_7_DDI_SUPPORTED \
    ((((UINT64)D3D11_0_7_DDI_INTERFACE_VERSION) << 32) | \
    (((UINT64)D3D11_0_7_DDI_BUILD_VERSION) << 16))
 
#ifndef IS_D3D11_WIN7_INTERFACE_VERSION
#define IS_D3D11_WIN7_INTERFACE_VERSION( i ) (D3D11_0_7_DDI_INTERFACE_VERSION == i)
#endif 
```

### <a name="span-idinformation_exchangespanspan-idinformation_exchangespaninformation-exchange"></a><span id="information_exchange"></span><span id="INFORMATION_EXCHANGE"></span>信息交换

除了指定版本信息外，驱动程序的[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数还在运行时与驱动程序之间交换其他信息。

在调用驱动程序的[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数时，运行时会在[**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的**pAdapterCallbacks**成员中提供[**pfnQueryAdapterInfoCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryadapterinfocb)适配器回调函数。 用户模式显示驱动程序应调用**pfnQueryAdapterInfoCb**适配器回调函数以从显示微型端口驱动程序查询图形硬件功能。

运行时调用用户模式显示驱动程序的[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数（驱动程序的适配器特定的一个函数）来创建显示设备，用于处理渲染状态的集合和完成初始化。 初始化完成后，Direct3D 版本11运行时可以调用[显示器驱动程序提供的 Direct3D 版本11函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)，用户模式显示驱动程序可以调用[运行时提供的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

用户模式显示驱动程序的 CreateDevice （D3D10）函数是使用[**D3D10DDIARG\_CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构调用的，该结构的成员按以下方式设置，以初始化用户模式显示驱动程序的版本 11 DDI：

-   运行时将**接口**设置为运行时需要用户模式显示驱动程序的接口版本。

-   运行时将**版本**设置为一个数字，驱动程序可以使用该数字来确定生成运行时的时间。 例如，驱动程序可以使用版本号来区分与 Windows Vista 一起发布的运行时，并使用后续 Service Pack 发布的运行时，其中可能包含驱动程序所需的修补程序。

-   运行时设置**hRTDevice** ，以指定驱动程序回调到运行时时应使用的句柄。

-   运行时设置**hDrvDevice**以指定运行时在后续的驱动程序调用中使用的句柄。

-   运行时在**pKTCallbacks**点的[**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)结构中提供其特定于设备的回调函数的表。 用户模式显示驱动程序调用运行时提供的回调函数，以访问显示微型端口驱动程序中的内核模式服务。

-   用户模式显示驱动程序会在[**D3D11DDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)结构中返回**p11DeviceFuncs**点的设备特定函数的表。

-   运行时向**DXGIBaseDDI**点提供一个[**DXGI\_DDI\_BASE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)结构。 运行时和用户模式显示驱动程序将其[DirectX 图形基础结构](directx-graphics-infrastructure-ddi.md)提供到此结构中。

-   运行时将**hRTCoreLayer**设置为指定驱动程序在驱动程序调用运行时以访问 core Direct3D 10 功能时应使用的句柄（即，调用**p11UMCallbacks**成员指定的函数）。

-   运行时在[**D3D11DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_corelayer_devicecallbacks)结构中提供其核心回调函数的表， **P11UMCALLBACKS**指向的结构。 用户模式显示驱动程序调用运行时提供的核心回调函数以刷新状态。

 

 





