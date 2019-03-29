---
title: 建议的 DirectX 9.0 驱动程序支持
description: 建议的 DirectX 9.0 驱动程序支持
ms.assetid: 57b4dac8-c694-47ec-b5f9-19247b4de433
keywords:
- 未使用的通道将默认 WDK DirectX 9.0
- 通道的默认值 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0240c934f019cea6514bfe7d459a8f9be264fb70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562827"
---
# <a name="recommended-directx-90-driver-support"></a>建议的 DirectX 9.0 驱动程序支持


## <span id="ddk_recommended_directx_9_0_driver_support_gg"></span><span id="DDK_RECOMMENDED_DIRECTX_9_0_DRIVER_SUPPORT_GG"></span>


建议 DirectX 9.0 驱动程序设置的未使用的纹理格式信道的默认值。

### <a name="span-idsettingdefaultsforunusedchannelsoftextureformatsspanspan-idsettingdefaultsforunusedchannelsoftextureformatsspanspan-idsettingdefaultsforunusedchannelsoftextureformatsspansetting-defaults-for-unused-channels-of-texture-formats"></a><span id="Setting_Defaults_for_Unused_Channels_of_Texture_Formats"></span><span id="setting_defaults_for_unused_channels_of_texture_formats"></span><span id="SETTING_DEFAULTS_FOR_UNUSED_CHANNELS_OF_TEXTURE_FORMATS"></span>未使用通道的纹理格式设置默认值

驱动程序和其设备应集中未使用的通道的默认值的纹理格式，以便应用程序可以依赖于已知存在的值由输入纹理不提供这些通道中。

参考光栅器适用于 DirectX 8.1 和更高版本中 D3DFMT 设置的默认值为未使用的 B 通道的方式类似于\_1.0f G16R16 纹理格式 (请参阅*refrast.cpp*示例代码)，DirectX9.0 版本驱动程序应设置为 1.0f 以下的 DirectX 9.0 浮点纹理格式中未使用的通道的默认值：

-   D3DFMT\_R16F

-   D3DFMT\_G16R16F

-   D3DFMT\_R32F

-   D3DFMT\_G32R32F

DirectX 9.0 驱动程序还应设置以下默认值：

-   Alpha 通道 (A) （透明度） 到 1.0 f，是不透明的。

-   到 1.0，这样就生成了一个最大的光线强度 f 的亮度通道 (L)。

参考光栅器还设置默认值为 B 通道，此外到一个通道，（的 RGBA) 为 1.0f D3DFMT\_V16U16 格式。 这样一来，D3DFMT\_V16U16 格式进行互换操作与 D3DFMT\_L6V5U5 格式，实际上有左通道。 在 D3DFMT\_L6V5U5 格式亮度位于 B 通道。

 

 





