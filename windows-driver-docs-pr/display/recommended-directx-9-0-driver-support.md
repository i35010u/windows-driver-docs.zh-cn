---
title: 建议的 DirectX 9.0 驱动程序支持
description: 建议的 DirectX 9.0 驱动程序支持
keywords:
- 未使用的通道默认值 WDK DirectX 9。0
- 通道默认值 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b884c97288832a2fcb7261bbc570b268d525d589
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810079"
---
# <a name="recommended-directx-90-driver-support"></a>建议的 DirectX 9.0 驱动程序支持


## <span id="ddk_recommended_directx_9_0_driver_support_gg"></span><span id="DDK_RECOMMENDED_DIRECTX_9_0_DRIVER_SUPPORT_GG"></span>


建议将 DirectX 9.0 驱动程序设置为不使用的纹理格式通道的默认值。

### <a name="span-idsetting_defaults_for_unused_channels_of_texture_formatsspanspan-idsetting_defaults_for_unused_channels_of_texture_formatsspanspan-idsetting_defaults_for_unused_channels_of_texture_formatsspansetting-defaults-for-unused-channels-of-texture-formats"></a><span id="Setting_Defaults_for_Unused_Channels_of_Texture_Formats"></span><span id="setting_defaults_for_unused_channels_of_texture_formats"></span><span id="SETTING_DEFAULTS_FOR_UNUSED_CHANNELS_OF_TEXTURE_FORMATS"></span>设置未使用的纹理格式通道的默认值

驱动程序及其设备应为未使用的通道设置默认值，以使应用程序可以依赖于输入纹理未提供的通道中存在的已知值。

类似于 DirectX 8.1 和更高版本的引用光栅程序将 D3DFMT G16R16 纹理格式的未使用的 B 通道的默认值设置 \_ 为 1.0 f (参阅 *refrast* 示例代码) ，directx 9.0 版本驱动程序应将以下 directx 9.0 浮点纹理格式中未使用的通道的默认值设置为 1.0 f：

-   D3DFMT \_ R16F

-   D3DFMT \_ G16R16F

-   D3DFMT \_ R32F

-   D3DFMT \_ G32R32F

DirectX 9.0 驱动程序还应设置以下默认值：

-   Alpha 通道 (透明度) 到 1.0 f 的)  (，这是不透明的。

-   亮度通道 (L) 为 1.0 f，这会产生最大的光线强度。

 (除了 D3DFMT V16U16 格式的 RGBA) 为 1.0 f 外，参考光栅还会为 B 通道设置默认值 \_ 。 通过这种方式，D3DFMT \_ V16U16 格式可与 D3DFMT \_ L6V5U5 格式互换，后者实际上具有 L 通道。 在 D3DFMT \_ L6V5U5 格式中，亮度置于 B 通道中。

 

 





