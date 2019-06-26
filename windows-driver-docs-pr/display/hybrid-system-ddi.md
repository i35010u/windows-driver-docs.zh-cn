---
title: 混合系统 DDI
description: 从 Windows 8.1 开始，这些用户模式和内核模式的结构和枚举显示设备驱动程序接口 (DDI) 已更新以处理跨适配器 D3D10_DDI_RESOURCE_MISC_FLAGD3DDDI_RESOURCEFLAGS2D3DDDI_ 的混合系统上的资源SYNCHRONIZATIONOBJECT_FLAGSD3DKMDT_GDISURFACEDATAD3DKMDT_GDISURFACETYPEDXGK_DRIVERCAPSDXGK_VIDMMCAPSThis 函数，Windows 8.1 的新增功能由用户模式显示驱动程序 QueryDListForApplication1 实现。
ms.assetid: 8AABE677-2C2D-4CFD-AF22-06D65524A158
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab47c69133bed7a19a67c88923f34fe3d7207e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380199"
---
# <a name="hybrid-system-ddi"></a>混合系统 DDI


从 Windows 8.1 开始，这些用户模式和内核模式的结构和枚举显示设备驱动程序接口 (DDI) 已更新以处理[跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)上[混合系统](using-cross-adapter-resources-in-a-hybrid-system.md):

-   [**D3D10\_DDI\_RESOURCE\_MISC\_FLAG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DKMDT\_GDISURFACEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)
-   [**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)

此函数中，Windows 8.1 的新用户模式驱动程序实现：

-   [*QueryDListForApplication1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)

下面介绍了如何设置并将注册的 DLL 的导出此函数。
## <a name="span-idsettingupthedlistdllspanspan-idsettingupthedlistdllspanspan-idsettingupthedlistdllspansetting-up-the-dlist-dll"></a><span id="Setting_up_the_dList_DLL"></span><span id="setting_up_the_dlist_dll"></span><span id="SETTING_UP_THE_DLIST_DLL"></span>设置能够关闭 dList DLL


一个*能够关闭 dList*是分立的 GPU 上的高性能渲染的需要跨适配器共享图面的应用程序的列表。 分立的 GPU 安装一个单独的较小**能够关闭 dList**将导出的 DLL [ **QueryDListForApplication1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)函数。 操作系统本身不会确定应用程序的运行在 GPU。 相反，Microsoft Direct3D 运行时调用**QueryDListForApplication1**在 Direct3D 初始化过程中最多一次。

该驱动程序必须查询进程的信息来确定进程需要是分立的 GPU，而不是集成的 GPU 的增强的性能的最新列表。

为了获得最佳性能的 DLL，应在 200 KB 大小，应保持在最低限度，分配并应该能够从返回[ **QueryDListForApplication1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_querydlistforapplication1)低于 4 毫秒中的函数。

## <a name="span-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanspan-idregisteringthedlistdllspanregistering-the-dlist-dll"></a><span id="Registering_the_dList_DLL"></span><span id="registering_the_dlist_dll"></span><span id="REGISTERING_THE_DLIST_DLL"></span>注册能够关闭 dList DLL


用户模式显示驱动程序提供的名称的少量**能够关闭 dList**注册表项下其 INF 文件中的 DLL **UserModeDListDriverName**和**UserModeDListDriverNameWow，** 在后一种**Wow64**注册表项。 下面是示例 INF 代码：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, UserModeDListDriverName,    %REG_MULTI_SZ%, dlistumd.dll
HKR,, UserModeDListDriverNameWow, %REG_MULTI_SZ%, dlistumdwow.dll
```
