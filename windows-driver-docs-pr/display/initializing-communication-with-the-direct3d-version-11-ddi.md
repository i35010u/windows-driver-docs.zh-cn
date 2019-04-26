---
title: 初始化与 Direct3D 版本 11 DDI 之间的通信
description: 初始化与 Direct3D 版本 11 DDI 之间的通信
ms.assetid: 3b383f78-da88-4979-b55f-8e234f230df7
keywords:
- Direct3D 11 版 WDK Windows 7 显示，初始化 DDI 通信
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，初始化 DDI 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74d6c0c926b04793a2fc26f1fc28d0a914d72b06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325042"
---
# <a name="initializing-communication-with-the-direct3d-version-11-ddi"></a>初始化与 Direct3D 版本 11 DDI 之间的通信


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

初始化与用户模式显示驱动程序 DLL 的版本 11 通信 DDI，Direct3D 11 版运行时首次加载 DLL 如果尚未加载该 DLL。 Direct3D 运行时接下来将调用用户模式显示驱动程序[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)函数通过 DLL 的导出表以打开图形适配器的实例。 **OpenAdapter10\_2**函数仅用于 DLL 的导出函数。

**请注意**   [ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)函数等同于[ **OpenAdapter10** ](https://msdn.microsoft.com/library/windows/hardware/ff568602)只不过**OpenAdapter10\_2**返回一个表中的驱动程序的特定于适配器的函数**pAdapterFuncs\_2**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)结构，并且**OpenAdapter10**返回一个表中的驱动程序的特定于适配器的函数pAdapterFuncs 隶属 D3D10DDIARG\_OPENADAPTER。 **pAdapterFuncs\_2**指向[ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)结构;**pAdapterFuncs**指向[ **D3D10DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541811)结构。

 

[**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)设计以便更有效地初始化驱动程序。 必须实现**OpenAdapter10\_2** Direct3D 11 版驱动程序中。 您还可以实现**OpenAdapter10\_2** (而非或除了[ **OpenAdapter10**](https://msdn.microsoft.com/library/windows/hardware/ff568602)) 在你的 Direct3D 版本 10.1 驱动程序，以提高初始化这些驱动程序的效率。 有关实现详细信息**OpenAdapter10\_2**在 Direct3D 版本 10.1 驱动程序，请参阅[版本发现支持](version-discovery-support.md)。 **OpenAdapter10\_2**处理版本控制和运行时和驱动程序之间的其他信息的交换。

### <a name="span-idversioningspanspan-idversioningspanversioning"></a><span id="versioning"></span><span id="VERSIONING"></span>版本控制

[**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)和驱动程序的特定于适配器的功能更改之间的 Direct3D API 和 Direct3D DDI 的版本控制处理的一种方式的 Direct3D 10 的方式处理版本控制 （有关详细信息有关 Direct3D 10 处理版本控制的方式，请参阅[与 Direct3D 版本 10 DDI 初始化通信](initializing-communication-with-the-direct3d-version-10-ddi.md))。 而不是依赖于失败的驱动程序的 Direct3D API **OpenAdapter10\_2**函数来指示特定版本不支持 (如同**OpenAdapter10\_2**)它支持 DDI 版本都必须显式列出驱动程序。 Direct3D 运行时将调用用户模式显示驱动程序[ **GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff566807) DDI 版本驱动程序支持的查询函数 （驱动程序的特定于适配器的功能之一）。

有至少两个新 DDI 版本的 Direct3D 11 DDI 函数。 每个 DDI 版本区分是否 DDI 在 Windows Vista 或 Windows 7 上运行。 但是，支持 Direct3D 11 DDI 并不一定表示完全支持的硬件功能所带来的 D3D\_功能\_级别\_11。 驱动程序可以支持新的线程 Direct3D 11 DDI 与不支持 Direct3D 11 DDI 等分割，公开的其他功能的硬件功能。 下面的代码演示如何区分每个 DDI 版本：

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

### <a name="span-idinformationexchangespanspan-idinformationexchangespaninformation-exchange"></a><span id="information_exchange"></span><span id="INFORMATION_EXCHANGE"></span>信息交换

除了指定版本信息，该驱动程序[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)函数也可交换之间运行时和驱动程序的其他信息。

对驱动程序的调用中[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)函数，运行时会提供[ **pfnQueryAdapterInfoCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568920)适配器中的回调函数**pAdapterCallbacks**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)结构。 用户模式显示驱动程序应调用**pfnQueryAdapterInfoCb**适配器回调函数来查询的图形硬件功能中的显示微型端口驱动程序。

运行时调用用户模式显示驱动程序[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)函数 （驱动程序的特定于适配器的功能之一） 创建用于处理的呈现状态集合的显示设备并完成初始化。 Direct3D 11 版运行时初始化完成后，可以调用[显示驱动程序提供的 Direct3D 版本 11 函数](https://msdn.microsoft.com/library/windows/hardware/ff552924)，并且用户模式显示驱动程序可以调用[运行时提供的函数](https://msdn.microsoft.com/library/windows/hardware/ff552862).

使用调用用户模式显示驱动程序的 CreateDevice(D3D10) 函数[ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)其成员设置按以下方式来初始化的结构用户模式显示驱动程序版本 11 DDI:

-   运行时设置**接口**到运行时需要从用户模式显示驱动程序接口的版本。

-   运行时设置**版本**驱动程序可用于标识时，运行时生成的数字。 例如，驱动程序可以使用的版本号随 Windows Vista 一起发布的运行时和后续的 service pack，其中可能包含驱动程序需要的修补程序发布的运行时之间进行区分。

-   运行时设置**hRTDevice**来指定当驱动程序回调到运行时，应使用该驱动程序的句柄。

-   运行时设置**hDrvDevice**在后续的驱动程序调用中指定运行时使用的句柄。

-   运行时会提供在其设备特定的回调函数的表[ **D3DDDI\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff544512)向其结构**pKTCallbacks**点. 用户模式显示驱动程序调用访问显示微型端口驱动程序中的内核模式服务的运行时提供的回调函数。

-   用户模式显示驱动程序将返回一个表中其特定于设备的函数[ **D3D11DDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff542141)向其结构**p11DeviceFuncs**点。

-   运行时会提供[ **DXGI\_DDI\_基本\_ARGS** ](https://msdn.microsoft.com/library/windows/hardware/ff557485)向其结构**DXGIBaseDDI**点。 在运行时和用户模式显示驱动程序提供其[DirectX 图形基础结构 DDI](directx-graphics-infrastructure-ddi.md)此结构。

-   运行时设置**hRTCoreLayer**以指定驱动程序时驱动程序回调到访问核心 Direct3D 10 功能的运行时应使用的句柄 (即，在调用函数的**p11UMCallbacks**成员指定)。

-   运行时会提供在其核心回调函数的表[ **D3D11DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff542137)结构到**p11UMCallbacks**点。 用户模式显示驱动程序调用运行时提供核心回调函数来刷新状态。

 

 





