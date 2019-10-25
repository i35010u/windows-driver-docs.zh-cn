---
title: 版本发现支持
description: 版本发现支持
ms.assetid: 9e37eaad-02b2-43a9-bd1a-4c5b2b02d1b6
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，版本发现支持
- 版本发现支持 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e361febcc217d14d63aa2b8cc70a6d0d50f48ca0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825297"
---
# <a name="version-discovery-support"></a>版本发现支持


本部分仅适用于 Windows 7 及更高版本的操作系统。

在 Windows Vista 及更高版本和 Windows Server 2008 及更高版本上运行的用户模式显示驱动程序必须无法为驱动程序未显式的 DDI 版本创建适配器（即，无法调用驱动程序的[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数）支持.

Windows 7 为 Direct3D 应用程序提供了一种方法，用于发现该驱动程序明确支持的 DDI 版本和硬件功能。 这可以改进版本验证。 Windows 7 引入了新的适配器特定的功能来改进版本，并提供了优化 API 和驱动程序初始化的机会。 你必须在 Direct3D 版本10.1 驱动程序中实现并导出[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)功能，使 direct3d 运行时可以调用驱动程序的新的适配器特定函数。 如果你改为在 Direct3D 版本10.1 驱动程序中实现[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) ，则驱动程序只能通过将调用传递到**OpenAdapter10**或对其进行调用来指示它是否支持 DDI 版本。

[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)返回[**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的**pAdapterFuncs\_2**成员中驱动程序的适配器特定函数的表。 **pAdapterFuncs\_2**指向[**D3D10\_2DDI\_ADAPTERFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs)结构。 Direct3D 运行时调用驱动程序的特定于适配器的[**GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)函数来查询驱动程序支持的 DDI 版本和硬件功能。 **GetSupportedVersions**在64位值的数组中返回 DDI 版本和硬件功能。 下面的代码示例演示了**GetSupportedVersions**实现：

```cpp
// Array of 64-bit values that are defined in D3d10umddi.h
const UINT64 c_aSupportedVersions[] = {
    D3D10_0_7_DDI_SUPPORTED, // 10.0 on Windows 7
    D3D10_0_DDI_SUPPORTED, // 10.0 on Windows Vista
 D3D10_1_x_DDI_SUPPORTED, // 10.1 with all extended 
                           // format support (but not
                           // Windows 7 scheduling)
};

HRESULT APIENTRY GetSupportedVersions(
                 D3D10DDI_HADAPTER hAdapter, 
                 __inout UINT32* puEntries,
 __out_ecount_opt( *puEntries ) 
 UINT64* pSupportedDDIInterfaceVersions)
)
{
    const UINT32 uEntries = ARRAYSIZE( c_aSupportedVersions );
    if (pSupportedDDIInterfaceVersions &&
        *puEntries < uEntries)
    {
        return HRESULT_FROM_WIN32( ERROR_INSUFFICIENT_BUFFER );
    }

    // Determine concise hardware support from kernel, cache with hAdapter.
    // pfnQueryAdapterInfoCb( hAdapter, ... )

    *puEntries = uEntries;
    if (pSupportedDDIInterfaceVersions)
    {
        UINT64* pCurEntry = pSupportedDDIInterfaceVersions;
        memcpy( pCurEntry, c_aSupportedVersions, sizeof( c_aSupportedVersions ) );
        pCurEntry += ARRAYSIZE( c_aSupportedVersions );
        assert( pCurEntry - pSupportedDDIInterfaceVersions == uEntries );
    }
    return S_OK;
}
```

不需要使用 Direct3D 版本10.1 驱动程序来验证传递到[ **\_D3D10DDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)的**接口**和**version**成员的值，并调用其[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)函数这些值包含用于初始化驱动程序的 DDI 版本信息。 驱动程序可以通过调用其[**GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)函数返回 DDI 版本和硬件功能。

在对驱动程序的[**CREATEDEVICE （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用**中，Direct3D**运行时可以将值传递给[**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice) **，这些**值不同于运行时传递到[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter);运行时将值传递给 D3D10DDIARG\_CREATEDEVICE 的**接口**和**版本**成员，这些值基于该驱动程序的[**GetSupportedVersions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)返回的 DDI 版本和硬件功能信息到运行时。 驱动程序无需验证传递到\_D3D10DDIARG 的**接口**和**Version**成员的值，因为驱动程序已通过其 GetSupportedVersions 指示了这些值的支持函数。

如果要将驱动程序从 Direct3D 版本10.0 移植到 Direct3D 版本10.1，则应将驱动程序转换为仅监视传递给[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)的**接口**和**版本**成员，而不是[**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)。 你应分析端口驱动程序**中的** [**CalcPrivateDeviceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)和**CreateDevice （D3D10）** 函数实现，以确保不会假设 *CreateDevice （D3D10）* ，用于匹配**OpenAdapter10\_2**的**Interface**和**Version**成员中的值。

**请注意**，  [**OpenAdapter10\_2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)的函数签名与[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) （即*D3d10umddi*标头中定义的 PFND3D10DDI\_OPENADAPTER 相同。 可以在同一个用户模式显示驱动程序 DLL 中实现这两个函数。

 

 

 





