---
title: 混合系统 DDI
description: 从 Windows 8.1 开始，会更新显示设备驱动程序接口（DDI）的这些用户模式和内核模式结构和枚举，以处理混合系统上的跨适配器资源 D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 函数 new for Windows 8.1，由用户模式显示驱动程序 QueryDListForApplication1 实现。
ms.assetid: 8AABE677-2C2D-4CFD-AF22-06D65524A158
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 700d4731bb251afd5db4a3600fe94fd94432060b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838893"
---
# <a name="hybrid-system-ddi"></a>混合系统 DDI


从 Windows 8.1 开始，会更新显示设备驱动程序接口（DDI）的这些用户模式和内核模式结构和枚举，以处理[混合系统](using-cross-adapter-resources-in-a-hybrid-system.md)上的[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)：

-   [**D3D10\_DDI\_资源\_杂项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)
-   [**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)

此函数是 Windows 8.1 的新功能，由用户模式显示驱动程序实现：

-   [*QueryDListForApplication1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)

下面介绍如何设置和注册导出此函数的 DLL。
## <a name="span-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspanspan-idsetting_up_the_dlist_dllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>设置 dList DLL


*DList*是一个应用程序列表，这些应用程序需要跨适配器共享图面，以便在离散 GPU 上呈现高性能。 离散 GPU 安装一个单独的小型**dList** DLL，该 DLL 将导出[**QueryDListForApplication1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)函数。 操作系统本身并不确定应用程序应运行的 GPU。 相反，Microsoft Direct3D 运行时在 Direct3D 初始化期间最多调用**QueryDListForApplication1** 。

驱动程序必须查询最新的进程信息列表，以确定进程是否需要离散 GPU 的增强性能，而不是集成 GPU。

为了获得最佳性能，DLL 大小应小于 200 KB，应保持最小分配，并且应能够从[**QueryDListForApplication1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)函数在4毫秒内返回。

## <a name="span-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanspan-idregistering_the_dlist_dllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>注册 dList DLL


用户模式显示驱动程序在其 INF 文件中的注册表项 " **UserModeDListDriverName** " 和 "UserModeDListDriverNameWow" 下提供了小型**dList** DLL 的名称 **，** 后者位于**Wow64**注册表项下。 下面是示例 INF 代码：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
