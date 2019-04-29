---
title: 版本发现支持
description: 版本发现支持
ms.assetid: 9e37eaad-02b2-43a9-bd1a-4c5b2b02d1b6
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示版本发现支持
- 版本发现支持 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682d5fbf0dc3c5ef0d90561459d52b0ee73eb01b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390797"
---
# <a name="version-discovery-support"></a>版本发现支持


本部分仅适用于 Windows 7 和更高版本的操作系统。

在 Windows Vista 和更高版本和 Windows Server 2008 和更高版本运行的用户模式显示驱动程序时不能适配器创建 (即，失败的驱动程序调用[ **OpenAdapter10** ](https://msdn.microsoft.com/library/windows/hardware/ff568602)函数） 的驱动程序不显式支持 DDI 版本。

Windows 7 提供的 Direct3D 应用程序发现 DDI 版本和驱动程序显式支持的硬件功能的方法。 这提高了版本验证。 Windows 7 引入了新的特定于适配器的函数来改善版本控制并提供机会来优化 API 和驱动程序初始化。 必须实现和导出[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603) Direct3D 版本 10.1 驱动程序以便 Direct3D 运行时可以调用驱动程序的新的特定于适配器的函数中的函数。 如果改为实现[ **OpenAdapter10** ](https://msdn.microsoft.com/library/windows/hardware/ff568602)在 Direct3D 版本 10.1 驱动程序，驱动程序可以并仅指示它是否支持 DDI 版本通过或未通过调用由**OpenAdapter10**。

[**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)返回的表中的驱动程序的特定于适配器的函数**pAdapterFuncs\_2**隶属[ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)结构。 **pAdapterFuncs\_2**指向[ **D3D10\_2DDI\_ADAPTERFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff541900)结构。 Direct3D 运行时将调用驱动程序的特定于适配器[ **GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff566807) DDI 版本和驱动程序支持的硬件功能的查询函数。 **GetSupportedVersions** 64 位值的数组中返回的 DDI 版本和硬件功能。 下面的代码示例演示**GetSupportedVersions**实现：

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

Direct3D 版本 10.1 驱动程序不需要验证的值传递给**接口**并**版本**的成员[ **D3D10DDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff541724)调用中其[ **OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)函数即使这些值包含用于对 DDI 版本信息初始化的驱动程序。 该驱动程序可以返回 DDI 版本和硬件功能，通过调用其[ **GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff566807)函数。

Direct3D 运行时可以传递到值**接口**并**版本**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)驱动程序的调用中[ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)不同于在运行时传递给的值的函数[ **OpenAdapter10\_2**](https://msdn.microsoft.com/library/windows/hardware/ff568603); 在运行时将值传递到**接口**并**版本**D3D10DDIARG 成员\_基于 DDI 的 CREATEDEVICE版本和硬件功能信息的驱动程序的[ **GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff566807)返回到运行时。 该驱动程序不需要验证传递给的值**接口**并**版本**D3D10DDIARG 成员\_CREATEDEVICE 因为驱动程序已指示的支持这些值通过其**GetSupportedVersions**函数。

如果要移植到 Direct3D 版本 10.1 驱动程序从 Direct3D 版本 10.0，则应将驱动程序只监视**接口**并**版本**成员传递给[**CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)而不是[ **OpenAdapter10\_2**](https://msdn.microsoft.com/library/windows/hardware/ff568603)。 您应分析两者[ **CalcPrivateDeviceSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538288)并**CreateDevice(D3D10)** 函数中以确保不不存在任何假设您已移植的驱动程序的实现有关中的值**接口**并**版本**的成员*CreateDevice(D3D10)* 匹配中的值**接口**并**版本**的成员**OpenAdapter10\_2**。

**请注意**  [**OpenAdapter10\_2** ](https://msdn.microsoft.com/library/windows/hardware/ff568603)具有相同的函数签名[ **OpenAdapter10** ](https://msdn.microsoft.com/library/windows/hardware/ff568602) （即，PFND3D10DDI\_中定义的 OPENADAPTER *D3d10umddi.h*标头)。 您可以在同一个用户模式显示驱动程序 DLL 中实现这两个函数。

 

 

 





