---
title: 混合系统 DDI
description: 从 Windows 8.1 开始，会更新显示设备驱动程序接口)  (的用户模式和内核模式结构和枚举，以处理混合系统上的跨适配器资源 D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 函数（新的 Windows 8.1）由用户模式显示驱动程序 QueryDListForApplication1 实现。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 036505a6436898bf1a11d778f56971eff85cd492
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793017"
---
# <a name="hybrid-system-ddi"></a>混合系统 DDI


从 Windows 8.1 开始，会更新显示设备驱动程序接口)  (的用户模式和内核模式结构和枚举，以处理[混合系统](using-cross-adapter-resources-in-a-hybrid-system.md)上的[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)：

-   [**D3D10 \_ DDI \_ 资源 \_ 杂项 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3DDDI \_ RESOURCEFLAGS2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDI \_ SYNCHRONIZATIONOBJECT \_ 标志**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DKMDT \_ GDISURFACEDATA**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)
-   [**D3DKMDT \_ GDISURFACETYPE**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)
-   [**DXGK \_ DRIVERCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK \_ VIDMMCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)

此函数是 Windows 8.1 的新功能，由用户模式显示驱动程序实现：

-   [*QueryDListForApplication1*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)

下面介绍如何设置和注册导出此函数的 DLL。
## <a name="span-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>设置 dList DLL


*DList* 是一个应用程序列表，这些应用程序需要跨适配器共享图面，以便在离散 GPU 上呈现高性能。 离散 GPU 安装一个单独的小型 **dList** DLL，该 DLL 将导出 [**QueryDListForApplication1**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1) 函数。 操作系统本身并不确定应用程序应运行的 GPU。 相反，Microsoft Direct3D 运行时在 Direct3D 初始化期间最多调用 **QueryDListForApplication1** 。

驱动程序必须查询最新的进程信息列表，以确定进程是否需要离散 GPU 的增强性能，而不是集成 GPU。

为了获得最佳性能，DLL 大小应小于 200 KB，应保持最小分配，并且应能够从 [**QueryDListForApplication1**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1) 函数在4毫秒内返回。

## <a name="span-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>注册 dList DLL


用户模式显示驱动程序在其 INF 文件中的注册表项 " **UserModeDListDriverName** " 和 "UserModeDListDriverNameWow" 下提供了小型 **dList** DLL 的名称 **，** 后者位于 **Wow64** 注册表项下。 下面是示例 INF 代码：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
