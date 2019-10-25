---
title: 支持 DXGI DDI
description: 支持 DXGI DDI
ms.assetid: 3a49d7cb-984f-4e4f-a549-5c0442e1c45a
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0f388df9532b103f0f740b878b3e987c45932a54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825595"
---
# <a name="supporting-the-dxgi-ddi"></a>支持 DXGI DDI


若要支持 Microsoft DirectX 图形基础结构（DXGI）设备驱动程序接口（DDI），用户模式显示驱动程序必须包含 Dxgiddi 头文件。 Dxgiddi 还包括 Dxgitype 标头文件，该文件包含与应用程序级 DXGI 构造共享的定义。 Dxgiddi 定义了多个用户模式显示驱动程序入口点和一个 DXGI 回调函数，驱动程序可以使用该函数与内核（包括显示微型端口驱动程序）进行通信。

Microsoft Direct3D runtime 提供对 Dxgi 中 DXGI DDI 的访问权限， [ **\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)结构， [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的**DXGIBaseDDI**成员在调用[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。 用户模式显示驱动程序提供了指向 DXGI 函数的指针。

驱动程序通过**pDXGIDDIBaseFunctionsXxx**成员 **\_DDI\_BASE\_参数**指向的结构的成员实现这些函数。 驱动程序应记录指向[dxgi 回调函数表](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的指针，该函数**将** **dxgi\_DDI\_BASE\_参数**指向以供以后使用。 驱动程序应将指针记录到 DXGI 回调函数表，而不是将单个指针记录到 DXGI 回调函数，因为 Direct3D 运行时可以在用户模式显示驱动程序。
软件 rasterizers 存在更多的 DXGI 用户模式显示驱动程序要求。 此类用户模式显示驱动程序（更具体而言，不支持与图形适配器上的 Direct3D 版本 9 DDI 实现共享的硬件的任何驱动程序）必须返回**DXGI\_状态\_no\_重定向**值，而不是[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的值\_OK 值。 返回**dxgi\_状态\_没有\_重定向**向 dxgi 指示，它不应使用共享资源表示路径来影响与桌面窗口管理器（DWM）的通信。 共享资源表示路径是在调用共享资源函数（即[**CreateResource （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)和[**OpenResource （D3D10）函数）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openresource)时创建的，而\_该函数 **\_资源\_杂项\_** 已设置共享标志）。 但是，DXGI 应该使用与存在相关的技术，其缓冲区仅可用于 CPU。 例如，DXGI 应通过除共享资源表示路径以外的其他方式将呈现的数据从后台缓冲区移动到桌面。 在这种情况下，DXGI 实际上会调用驱动程序的[**PresentDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数来移动呈现的数据，而不是影响与 DWM 的通信。

## <a name="direct3d-version-10-dxgi-functions"></a>Direct3D 版本 10 DXGI 函数

本部分介绍用户模式显示驱动程序 DLL 提供给 Microsoft Direct3D 版本10运行时的 Microsoft DirectX 图形基础结构（DXGI）函数。 驱动程序在对用户模式显示驱动程序的[CreateDevice （D3D10）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用中通过[DXGI_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)结构的成员提供指向 DXGI 函数的指针。

|||
|:--|:--|
|BltDXGI|GetGammaCapsDXGI|
|PresentDXGI|QueryResourceResidencyDXGI|
|ResolveSharedResourceDXGI|RotateResourceIdentitiesDXGI|
|SetDisplayModeDXGI|SetResourcePriorityDXGI|


## <a name="direct3d-version-111-dxgi-functions"></a>Direct3D 版本 11.1 DXGI 函数

本部分介绍用户模式显示驱动程序实现的 Microsoft DirectX 图形基础结构（DXGI）函数，这些函数是为 Microsoft Direct3D 版本11.1 运行时添加的。 Direct3D 11.1 随 Windows 8 一起引入。 

当运行时调用 CreateDevice （D3D10）时，用户模式显示驱动程序 DLL 将导出[OpenAdapter10_2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数，并通过[D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构的成员向适配器特定函数提供指针。

该驱动程序通过对用户模式显示驱动程序的特定于适配器的[CreateDevice （D3D10）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用，提供指向 Direct3D 版本 11.1 DXGI[函数的指针](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)。

|||
|:--|:--|
|Blt1DXGI|OfferResourcesDXGI|
|ReclaimResourcesDXGI||

## <a name="direct3d-version-112-dxgi-functions"></a>Direct3D 版本 11.2 DXGI 函数

本部分中的参考页面描述了由用户模式显示驱动程序实现的 Microsoft DirectX 图形基础结构（DXGI）函数，这些函数是为 Microsoft Direct3D 版本11.2 运行时添加的。 Windows 8.1 引入了 Direct3D 11.2。 

当运行时调用 CreateDevice （D3D10）时，用户模式显示驱动程序 DLL 将导出 OpenAdapter10_2 函数，并通过[D3D10_2DDI_ADAPTERFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构的成员向适配器特定函数提供指针。

该驱动程序通过对用户模式显示驱动程序的特定于适配器的[CreateDevice （D3D10）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用，提供指向 Direct3D 版本 11.2 DXGI[函数的指针](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)。

|||
|:--|:--|
|[PFNDDXGIDDI_PRESENT_MULTIPLANE_OVERLAYCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|[PFNDDXGIDDI_PRESENTCB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_presentcb)|
|[PFNDDXGIDDI_SUBMITPRESENTBLTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresentblttohwqueuecb)|[PFNDDXGIDDI_SUBMITPRESENTTOHWQUEUECB](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresenttohwqueuecb)|

> [!NOTE]
> Direct3D 11.2 运行时支持的其他 DXGI 函数包含在[用户模式驱动程序实现的 Multiplane 覆盖函数](multiplane-overlay-support.md)部分中。

