---
title: 版本发现支持
description: 版本发现支持
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，版本发现支持
- 版本发现支持 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0a9e3a391fde69b1aa26e66c88a321544845b13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792915"
---
# <a name="version-discovery-support"></a>版本发现支持


本部分仅适用于 Windows 7 及更高版本的操作系统。

在 Windows Vista 及更高版本和 Windows Server 2008 及更高版本上运行的用户模式显示驱动程序必须无法通过适配器创建 (也就是说，对驱动程序的 [**OpenAdapter10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) 函数的调用无法) ，因为该驱动程序不会显式支持该驱动程序。

Windows 7 为 Direct3D 应用程序提供了一种方法，用于发现该驱动程序明确支持的 DDI 版本和硬件功能。 这可以改进版本验证。 Windows 7 引入了新的适配器特定的功能来改进版本，并提供了优化 API 和驱动程序初始化的机会。 你必须在 Direct3D 版本10.1 驱动程序中实现和导出 [**OpenAdapter10 \_ 2**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) 功能，使 direct3d 运行时可以调用该驱动程序的新的适配器特定函数。 如果你改为在 Direct3D 版本10.1 驱动程序中实现 [**OpenAdapter10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) ，则驱动程序只能通过将调用传递到 **OpenAdapter10** 或对其进行调用来指示它是否支持 DDI 版本。

[**OpenAdapter10 \_ 2**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)返回 [**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)结构的 **pAdapterFuncs \_ 2** 成员中该驱动程序的适配器特定函数的表。 **pAdapterFuncs \_ 2** 指向 [**D3D10 \_ 2DDI \_ ADAPTERFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10_2ddi_adapterfuncs) 结构。 Direct3D 运行时调用驱动程序的特定于适配器的 [**GetSupportedVersions**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions) 函数来查询驱动程序支持的 DDI 版本和硬件功能。 **GetSupportedVersions** 在64位值的数组中返回 DDI 版本和硬件功能。 下面的代码示例演示了 **GetSupportedVersions** 实现：

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

不需要 Direct3D 版本10.1 驱动程序来验证传递给 [**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)的 **接口** 和 **version** 成员的值，即使这些值包含用于初始化驱动程序 [**的 \_**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) DDI 版本信息。 驱动程序可以通过调用其 [**GetSupportedVersions**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions) 函数返回 DDI 版本和硬件功能。

Direct3D 运行时可在对驱动程序的 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数（与运行时传递到 [**OpenAdapter10 \_ 2**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)的值不同的值）的调用中将值传递给 [**D3D10DDIARG \_ CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)的 **接口** 和 **版本** 成员; 运行时将值传递到 D3D10DDIARG CREATEDEVICE 的 **接口** 和 **版本** 成员，这些成员 \_ 基于驱动程序的 [**GetSupportedVersions**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10_2ddi_getsupportedversions)返回到运行时的 DDI 版本和硬件功能信息。 该驱动程序不需要验证传递给 D3D10DDIARG CREATEDEVICE 的 **接口** 和 **Version** 成员的值， \_ 因为该驱动程序已通过其 **GetSupportedVersions** 函数指出了这些值的支持。

如果要将驱动程序从 Direct3D 版本10.0 移植到 Direct3D 版本10.1，则应将驱动程序转换为仅监视传递到 [**CreateDevice (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)的 **接口** 和 **版本** 成员，而不是 [**OpenAdapter10 \_ 2**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)。 你应该分析你的移植驱动程序中的 [**CalcPrivateDeviceSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)和 **CreateDevice (D3D10)** 函数实现，以确保不会对与 **D3D10 \_ 2** 的 **interface** 和 **version** 成员中的值匹配的 **interface** 和 **version** *)  (* 成员中的值进行任何假设。

**请注意**，[**OpenAdapter10 \_ 2**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)的函数签名与 [**OpenAdapter10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter) (的函数签名相同，PFND3D10DDI \_ OPENADAPTER 在 *D3d10umddi* 标头) 中定义。   可以在同一个用户模式显示驱动程序 DLL 中实现这两个函数。

 

 

