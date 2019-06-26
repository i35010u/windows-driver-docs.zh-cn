---
title: 支持 DXGI DDI
description: 支持 DXGI DDI
ms.assetid: 3a49d7cb-984f-4e4f-a549-5c0442e1c45a
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed1f59b9608e2f1f372ec24093e4a5ab78438b9a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361233"
---
# <a name="supporting-the-dxgi-ddi"></a>支持 DXGI DDI


若要支持 Microsoft DirectX 图形基础结构 (DXGI) 的设备驱动程序接口 (DDI)，用户模式显示驱动程序必须包括 Dxgiddi.h 标头文件。 Dxgiddi.h 还包括 Dxgitype.h 标头文件，其中包含与应用程序级别共享定义 DXGI 构造。 Dxgiddi.h 定义多个用户模式显示驱动程序入口点和驱动程序可用于与内核 （包括显示微型端口驱动程序） 通信的 DXGI 回调函数。

Microsoft Direct3D 运行时会提供访问在 DXGI DDI [ **DXGI\_DDI\_基本\_ARGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)结构的**DXGIBaseDDI**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构在调用指向[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。 用户模式显示驱动程序提供了指向 DXGI 函数的指针。

该驱动程序实现的结构的成员通过这些函数的**pDXGIDDIBaseFunctionsXxx**的成员**DXGI\_DDI\_基本\_ARGS**指向。 该驱动程序应记录到指针[DXGI 回调函数表](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)的**pDXGIBaseCallbacks**的成员**DXGI\_DDI\_基本\_ARGS**指向以供将来使用。 驱动程序应记录到 DXGI 回调函数表指针而不是记录 DXGI 回调函数的单个指针，因为 Direct3D 运行时可以更改回调函数的地址，只要在没有线程用户模式显示驱动程序。
进一步 DXGI 用户模式显示驱动程序要求存在的软件光栅器。 此类用户模式下显示的驱动程序 （具体而言，任何驱动程序的执行不支持与图形适配器上的 Direct3D 版本 9 DDI 实现共享的是硬件） 必须返回**DXGI\_状态\_没有\_重定向**值而不是 S\_确定值从其[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。 返回**DXGI\_状态\_否\_重定向**指示 DXGI，它不应使用有效的交流的共享的资源的演示文稿路径与桌面窗口管理器 (DWM)。 时创建的共享的资源的演示文稿路径对共享资源函数的调用 (即[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)并[ **OpenResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openresource)函数与**D3D10\_DDI\_资源\_杂项\_共享**标志设置) 发生。 但是，DXGI 应改为使用其缓冲区为仅供 CPU swapchain 与相关的技术。 例如，DXGI 应呈现的数据从移动后台缓冲区到桌面的共享的资源的演示文稿路径之外的其他方法。 在此情况下，DXGI 实际调用的驱动程序[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数将呈现的数据而不是有效的交流与 DWM 移动。

## <a name="direct3d-version-10-dxgi-functions"></a>Direct3D 版本 10 DXGI 函数

本部分介绍用户模式下向 Microsoft Direct3D 版本 10 运行时显示驱动程序 DLL 提供的 Microsoft DirectX 图形基础结构 (DXGI) 函数。 驱动程序提供的成员通过 DXGI 函数的指针[DXGI_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)对用户模式显示驱动程序的调用中的结构[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

|||
|:--|:--|
|BltDXGI|GetGammaCapsDXGI|
|PresentDXGI|QueryResourceResidencyDXGI|
|ResolveSharedResourceDXGI|RotateResourceIdentitiesDXGI|
|SetDisplayModeDXGI|SetResourcePriorityDXGI|


## <a name="direct3d-version-111-dxgi-functions"></a>Direct3D 版本 11.1 DXGI 函数

本部分介绍 Microsoft DirectX 图形基础结构 (DXGI) 函数，由用户模式显示驱动程序，Microsoft Direct3D 版本 11.1 运行时添加的实现。 Direct3D 11.1 中引入了 Windows 8。 

用户模式显示驱动程序 DLL 导出[OpenAdapter10_2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数，并提供指向特定于适配器的函数的成员通过[D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构时运行时调用 CreateDevice(D3D10)。

驱动程序提供的成员通过 Direct3D 11.1 版本 DXGI 函数的指针[DXGI1_2_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)结构对用户模式显示驱动程序的调用中的特定于适配器的[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

|||
|:--|:--|
|Blt1DXGI|OfferResourcesDXGI|
|ReclaimResourcesDXGI||

## <a name="direct3d-version-112-dxgi-functions"></a>版本 Direct3D 11.2 DXGI 函数

在本部分中的参考页介绍了实现的用户模式显示驱动程序，Microsoft Direct3D 版本 11.2 运行时添加的 Microsoft DirectX 图形基础结构 (DXGI) 功能。 Direct3D 11.2 中引入了 Windows 8.1。 

用户模式显示驱动程序 DLL 导出 OpenAdapter10_2 函数，并提供指向的成员通过特定于适配器的函数的指针[D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构，当运行时调用 CreateDevice(D3D10)。

驱动程序提供的成员通过 Direct3D 11.2 版本 DXGI 函数的指针[DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)结构对用户模式显示驱动程序的调用中的特定于适配器的[CreateDevice (D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

|||
|:--|:--|
|[PFNDDXGIDDI_PRESENT_MULTIPLANE_OVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|[PFNDDXGIDDI_PRESENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_presentcb)|
|[PFNDDXGIDDI_SUBMITPRESENTBLTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresentblttohwqueuecb)|[PFNDDXGIDDI_SUBMITPRESENTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresenttohwqueuecb)|

> [!NOTE]
> 在部分中，包含由 Direct3D 11.2 运行时支持的其他 DXGI 函数[Multiplane 覆盖由用户模式驱动程序实现的函数](multiplane-overlay-support.md)。

