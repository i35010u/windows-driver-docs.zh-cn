---
title: 处理像素格式的颜色值
description: 处理像素格式的颜色值
keywords:
- 用于像素格式的颜色值 WDK DirectX 9。0
- 像素格式颜色值 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 915d135525639daf1ac636b9e52d5394053edb8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822503"
---
# <a name="handling-color-values-for-pixel-formats"></a>处理像素格式的颜色值


## <span id="ddk_handling_color_values_for_pixel_formats_gg"></span><span id="DDK_HANDLING_COLOR_VALUES_FOR_PIXEL_FORMATS_GG"></span>


**本主题适用于 DirectX 7.0 和更高版本。**

显示驱动程序必须转换颜色格式的 ARGB 和 YUV 类的输入颜色值，因为应用程序以统一的方式请求具有这些格式的图面上的颜色填充和清除操作。 但是，驱动程序必须直接从其他类格式使用颜色值。 例如，应用程序使用 A8R8G8B8 作为 alpha (的所有表面的统一颜色值：) ，红色 (R) ，绿色 (G) 和蓝色 () 组件;驱动程序必须通过复制具有最高重要性的位，将 A8R8G8B8 颜色转换为特定于实际 ARGB 格式的颜色值。

显示驱动程序在处理 \_ 其 D3dDrawPrimitives2 函数中的 D3DDP2OP CLEAR 和 D3DDP2OP \_ COLORFILL 操作代码 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)时接收颜色值。

显示驱动程序可以使用以下代码来转换 ARGB 和 YUV 类格式的颜色值：

```cpp
DWORD Convert2N(DWORD Color, DWORD n)
{
    return (Color * (1 << n)) / 256;
}

DWORD CPixel::ConvertFromARGB(D3DCOLOR  InputColor,
                              D3DFORMAT OutputFormat)
{
    DWORD Output = (DWORD) InputColor;
    DWORD Alpha = InputColor >> 24;
    DWORD Red = (InputColor >> 16) & 0x00ff;
    DWORD Green = (InputColor >> 8) & 0x00ff;
    DWORD Blue = InputColor & 0x00ff;
    switch(OutputFormat) {
    case D3DFMT_R8G8B8:
    case D3DFMT_X8R8G8B8:
        Output = InputColor & 0x00ffffff;
        break;

    case D3DFMT_A8R8G8B8:
        Output = InputColor;
        break;

    case D3DFMT_R5G6B5:
        Output = (Convert2N(Red,5) << 11) | 
                    (Convert2N(Green,6) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_X1R5G5B5:
        Output = (Convert2N(Red,5) << 10) | 
                    (Convert2N(Green,5) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_A1R5G5B5:
        Output = (Convert2N(Alpha, 1) << 15) | 
                    (Convert2N(Red,5) << 10) | 
                    (Convert2N(Green,5) << 5) | 
                    (Convert2N(Blue,5));
        break;

    case D3DFMT_X4R4G4B4:
        Output = (Convert2N(Red,4) << 8) | 
                    (Convert2N(Green,4) << 4) | 
                    (Convert2N(Blue,4));
        break;

    case D3DFMT_A4R4G4B4:
        Output = (Convert2N(Alpha,4) << 12) |
                    (Convert2N(Red,4) << 8) | 
                    (Convert2N(Green,4) << 4) | 
                    (Convert2N(Blue,4));
        break;

    case D3DFMT_R3G3B2:
        Output = (Convert2N(Red,3) << 5) | 
                    (Convert2N(Green,3) << 2) | 
                    (Convert2N(Blue,2));
        break;

    case D3DFMT_A8R3G3B2:
        Output = (Alpha << 8) |
                    (Convert2N(Red,3) << 5) | 
                    (Convert2N(Green,3) << 2) | 
                    (Convert2N(Blue,2));
        break;

    case D3DFMT_A2B10G10R10:
        Output = (Convert2N(Alpha,2) << 30) |
                    (Convert2N(Red,10)) | 
                    (Convert2N(Green,10) << 10) | 
                    (Convert2N(Blue,10) << 20);
        break;

    case D3DFMT_X8B8G8R8:
        Output = (Convert2N(Red,8)) | 
                    (Convert2N(Green,8) << 8) | 
                    (Convert2N(Blue,8) << 16);
        break;

    case D3DFMT_A8B8G8R8:
        Output = (Alpha << 24) |
                    (Convert2N(Red,8)) | 
                    (Convert2N(Green,8) << 8) | 
                    (Convert2N(Blue,8) << 16);
        break;

#if (DXPIXELVER > 8)
    case D3DFMT_A2R10G10B10:
        Output = (Convert2N(Alpha,2) << 30) |
                    (Convert2N(Red,10) << 20) | 
                    (Convert2N(Green,10) << 10) | 
                    (Convert2N(Blue,10));
        break;
#endif

    case D3DFMT_UYVY:
#if (DXPIXELVER > 8)
    case D3DFMT_R8G8_B8G8:
#endif
        Output = (Red << 24) |
                    (Green << 16) |
                    (Red << 8) |
                    (Blue);
        break;
 
    case D3DFMT_YUY2:
#if (DXPIXELVER > 8)
    case D3DFMT_G8R8_G8B8:
#endif
        Output = (Green << 24) |
                    (Red << 16) |
                    (Blue << 8) |
                    (Red);
        break;

    case MAKEFOURCC('A', 'Y', 'U', 'V'):
    case MAKEFOURCC('N', 'V', '1', '2'):
    case MAKEFOURCC('Y', 'V', '1', '2'):
    case MAKEFOURCC('I', 'C', 'M', '1'):
    case MAKEFOURCC('I', 'C', 'M', '2'):
    case MAKEFOURCC('I', 'C', 'M', '3'):
    case MAKEFOURCC('I', 'C', 'M', '4'):
        Output = InputColor;
        break;
    }
    return Output;
}
```

 

