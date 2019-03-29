---
title: 存在开销改进
ms.assetid: 92B282D6-0D04-4352-AE03-E0A7A43711E7
description: 对内部交换缓冲区以减少 GPU 处理负载的改进
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64bff6e8c3e9b7187e3ebf9daa0fe395b855533c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562216"
---
# <a name="present-overhead-improvements"></a>存在开销改进


从 Windows 8.1 开始，Microsoft Direct3D 运行时句柄内部交换缓冲区更多有效地减少在 GPU 上的处理负载。 若要支持此更好的性能，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序必须支持新存在设备驱动程序接口 (DDI) 和新的纹理格式作为共享图面：

## <a name="span-idwddm13presentddispanspan-idwddm13presentddispanwddm-13-present-ddi"></a><span id="wddm_1.3_present_ddi"></span><span id="WDDM_1.3_PRESENT_DDI"></span>WDDM 1.3 存在 DDI


这些参考主题介绍如何在您的显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*pfnPresent1(D3D)*](https://msdn.microsoft.com/library/windows/hardware/dn458010)
-   [*pfnPresent1(DXGI)*](https://msdn.microsoft.com/library/windows/hardware/dn469267)
-   [**D3DDDIARG\_PRESENT1**](https://msdn.microsoft.com/library/windows/hardware/dn457997)
-   [**D3DDDIARG\_PRESENTSURFACE**](https://msdn.microsoft.com/library/windows/hardware/dn457998)
-   [**D3DKMT\_组合\_PRESENTHISTORYTOKEN**](https://msdn.microsoft.com/library/windows/hardware/dn458001)
-   [**DXGI\_DDI\_ARG\_PRESENT1**](https://msdn.microsoft.com/library/windows/hardware/dn457714)
-   [**DXGI\_DDI\_ARG\_PRESENTSURFACE**](https://msdn.microsoft.com/library/windows/hardware/dn457715)
-   [**D3DDDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff544519) (新**pfnPresent1**函数指针)
-   [**D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312) (新**D3DDDIFMT\_G8R8**并**D3DDDIFMT\_R8**常量值)
-   [**D3DKMT\_存在\_模型**](https://msdn.microsoft.com/library/windows/hardware/ff548197) (新**D3DKMT\_PM\_重定向\_组合**常量值)
-   [**D3DKMT\_PRESENTHISTORYTOKEN** ](https://msdn.microsoft.com/library/windows/hardware/ff548188) (新**组合**成员)
-   [**DXGI\_DDI\_BASE\_ARGS** ](https://msdn.microsoft.com/library/windows/hardware/ff557485) (新**pDXGIDDIBaseFunctions4**成员)
-   [**DXGI1\_3\_DDI\_基\_函数**](https://msdn.microsoft.com/library/windows/hardware/dn465883) (新**pfnPresent1**函数指针)

## <a name="span-idtextureformatsupportforsharedsurfacesspanspan-idtextureformatsupportforsharedsurfacesspanspan-idtextureformatsupportforsharedsurfacesspantexture-format-support-for-shared-surfaces"></a><span id="Texture_format_support_for_shared_surfaces"></span><span id="texture_format_support_for_shared_surfaces"></span><span id="TEXTURE_FORMAT_SUPPORT_FOR_SHARED_SURFACES"></span>对于共享图面纹理格式支持


驱动程序应支持这两个共享资源和从这些额外纹理格式可共享后台缓冲区[ **DXGI\_格式**](https://msdn.microsoft.com/library/windows/desktop/bb173059)枚举：

- **DXGI\_FORMAT\_A8\_UNORM**
- **DXGI\_FORMAT\_R8\_UNORM**
- **DXGI\_FORMAT\_R8G8\_UNORM**
- **DXGI\_FORMAT\_BC1\_TYPELESS\\***
- **DXGI\_FORMAT\_BC1\_UNORM**
- **DXGI\_FORMAT\_BC1\_UNORM\_SRGB**
- **DXGI\_FORMAT\_BC2\_TYPELESS\\***
- **DXGI\_FORMAT\_BC2\_UNORM**
- **DXGI\_FORMAT\_BC2\_UNORM\_SRGB**
- **DXGI\_FORMAT\_BC3\_TYPELESS\\***
- **DXGI\_FORMAT\_BC3\_UNORM**
- **DXGI\_FORMAT\_BC3\_UNORM\_SRGB**

此外，驱动程序应支持**DXGI\_格式\_L8\_UNORM**占位符的格式如果它们支持 Microsoft Direct3D 11 和 Direct3D 功能级别 9 的硬件更高版本上。 **DXGI\_格式\_L8\_UNORM**功能上等效于**D3DDDIFMT\_L8**格式。

驱动程序还应支持从其他纹理格式[ **D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312)枚举：

-   **D3DDDIFMT\_G8R8**
-   **D3DDDIFMT\_R8**

 

 





