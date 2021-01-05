---
title: 支持 DXGI DDI
description: 支持 DXGI DDI
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad466a2a485a97313cbef3af44720d2cb38af757
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812495"
---
# <a name="supporting-the-dxgi-ddi"></a>支持 DXGI DDI

若要支持 Microsoft DirectX 图形基础结构 (DXGI) 设备驱动程序接口 (DDI) ，用户模式显示驱动程序必须包含 [*Dxgiddi*](/windows-hardware/drivers/ddi/dxgiddi) 头文件。 *Dxgiddi* 还包括 [*Dxgitype*](/windows-hardware/drivers/ddi/dxgitype) 标头文件，该文件包含与应用程序级 DXGI 构造共享的定义。 *Dxgiddi* 定义了多个用户模式显示驱动程序入口点和一个 DXGI 回调函数，驱动程序可以使用该函数与内核 (包括显示微型端口驱动程序) 进行通信。

Microsoft Direct3D 运行时提供对 [**DXGI_DDI_BASE_ARGS**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)结构中的 DXGI DDI 的访问， [**D3D10DDIARG_CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的 **DXGIBaseDDI** 成员在调用 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数时指向该函数。 用户模式显示驱动程序提供了指向 DXGI 函数的指针。

驱动程序通过 **pDXGIDDIBaseFunctionsXxx** 的成员 **DXGI_DDI_BASE_ARGS** 指向的结构成员来实现这些函数。 驱动程序应记录指向 DXGI 回调函数表的指针，该函数的 **pDXGIBaseCallbacks** 成员 **DXGI_DDI_BASE_ARGS** 指向该函数，以供以后使用。 驱动程序应记录到 DXGI 回调函数表的指针，而不是将单个指针记录到 DXGI 回调函数，因为在用户模式显示驱动程序中没有线程时，Direct3D 运行时可以更改回调函数的地址。

软件 rasterizers 存在更多的 DXGI 用户模式显示驱动程序要求。 此类用户模式显示驱动程序更具体 (，任何不支持在图形适配器上使用 Direct3D 版本 9 DDI 实现共享的硬件的驱动程序) 必须返回 **DXGI_STATUS_NO_REDIRECTION** 值，而不是从其 [**CreateDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice) 函数返回 S_OK 值。 此返回值向 DXGI 表明，它不应使用共享资源表示路径来影响与桌面窗口管理器 (DWM) 的通信。 共享资源表示路径是在调用共享资源函数时创建的， (即 [**CreateResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource) 和 [**OpenResource (D3D10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openresource) **) D3D10_DDI_RESOURCE_MISC_SHARED 标志设置**) 函数。 但是，DXGI 应该使用与存在相关的技术，其缓冲区仅可用于 CPU。 例如，DXGI 应通过除共享资源表示路径以外的其他方式将呈现的数据从后台缓冲区移动到桌面。 在这种情况下，DXGI 实际上会调用驱动程序的 [**PresentDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数来移动呈现的数据，而不是影响与 DWM 的通信。

## <a name="direct3d-version-10-dxgi-functions"></a>Direct3D 版本 10 DXGI 函数

本部分介绍了 (DXGI) 函数的 Microsoft DirectX 图形基础结构，用户模式显示驱动程序 DLL 提供此功能。 该驱动程序通过调用用户模式显示驱动程序的[CreateDevice (D3D10) ](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数，提供指向通过[DXGI_DDI_BASE_FUNCTIONS](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)结构的成员的 DXGI 函数的指针。

**BltDXGI**： GetGammaCapsDXGI

**PresentDXGI**： QueryResourceResidencyDXGI

**ResolveSharedResourceDXGI**： RotateResourceIdentitiesDXGI

**SetDisplayModeDXGI**： SetResourcePriorityDXGI

## <a name="direct3d-version-111-dxgi-functions"></a>Direct3D 版本 11.1 DXGI 函数

本部分介绍 Microsoft DirectX 图形基础结构 (DXGI) 函数，这些函数是由用户模式显示驱动程序实现的，这些功能是为 Microsoft Direct3D 版本11.1 运行时添加的。 Direct3D 11.1 随 Windows 8 一起引入。

当运行时调用 CreateDevice (D3D10) 时，用户模式显示驱动程序 DLL 会导出 [OpenAdapter10_2](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) 函数并通过 [D3D10_2DDI_ADAPTERFUNCS](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs) 结构的成员向特定于适配器的函数提供指针。

该驱动程序 [DXGI1_2_DDI_BASE_FUNCTIONS](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions) 通过调用用户模式显示驱动程序的特定于适配器的 [CreateDevice (D3D10) ](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice) 函数，提供指向 Direct3D 版本 11.1 DXGI 函数的指针。

## <a name="direct3d-version-112-dxgi-functions"></a>Direct3D 版本 11.2 DXGI 函数

本部分中的参考页介绍 Microsoft DirectX 图形基础结构 (DXGI) 函数，这些函数是由用户模式显示驱动程序实现的，这些功能是为 Microsoft Direct3D 版本11.2 运行时添加的。 Windows 8.1 引入了 Direct3D 11.2。

当运行时调用 CreateDevice (D3D10) 时，用户模式显示驱动程序 DLL 会导出 OpenAdapter10_2 函数并通过 [D3D10_2DDI_ADAPTERFUNCS](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs) 结构的成员向特定于适配器的函数提供指针。

该驱动程序 [DXGI1_3_DDI_BASE_FUNCTIONS](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) 通过调用用户模式显示驱动程序的特定于适配器的 [CreateDevice (D3D10) ](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice) 函数，提供指向 Direct3D 版本 11.2 DXGI 函数的指针。

**[PFNDDXGIDDI_PRESENT_MULTIPLANE_OVERLAYCB](/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)**： [PFNDDXGIDDI_PRESENTCB](/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_presentcb)

**[PFNDDXGIDDI_SUBMITPRESENTBLTTOHWQUEUECB](/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresentblttohwqueuecb)**： [PFNDDXGIDDI_SUBMITPRESENTTOHWQUEUECB](/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_submitpresenttohwqueuecb)

> [!NOTE]
> Direct3D 11.2 运行时支持的其他 DXGI 函数包含在 [用户模式驱动程序实现的 Multiplane 覆盖函数](multiplane-overlay-support.md)部分中。
