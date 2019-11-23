---
title: Windows 8.1 中的 YUV 格式范围
ms.assetid: D76FFB8C-CA42-446E-826F-52982B1849E5
description: 用户模式显示驱动程序如何利用 YUV 视频格式
keywords:
- 全范围 YUV WDK 显示
- 扩展范围 YUV WDK 显示
- studio 亮度范围 YUV WDK 显示
- YUV 格式和 WMF 支持 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8708358822f78f55563b1ff0120e10f86f9837e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829129"
---
# <a name="yuv-format-ranges-in-windows81"></a>Windows 8.1 中的 YUV 格式范围


应用可向用户模式显示驱动程序发出信号，以利用从 Windows 8.1 开始的扩展范围 \[0，255\] YUV 视频格式，如下表所示：

| YUV 范围                | 输入数据范围 | 典型用法                                           | Standard                                                  |
|--------------------------|------------------|---------------------------------------------------------|-----------------------------------------------------------|
| *扩展范围*         | \[0，255\]       | 消费者设备：网络摄像机和点和拍摄摄像头 | JFIF standard 和 MJPEG 视频格式使用作为默认值 |
| *studio 亮度范围* | \[16，235\]      | 职业相机和视频设备                | ITU BT. 601 和 BT。为709                                     |

 

内容和广播行业生成的大多数视频都在工作室范围内，而各个使用者生成的视频在扩展范围内。 "扩展范围" 也称为 "*完整亮度范围*"。

在 Windows 8.1 之前，Microsoft 媒体基础视频处理管道对所有输入数据进行操作，就像它在工作室范围内一样，这会导致动态范围下降，并且如果输入数据实际在扩展范围内，则通常会出现鲜明的对比度。

从 Windows 8.1 开始，当视频输入 YUV 格式在扩展范围内时，应用程序可以通知更高的动态范围的驱动程序。

## <a name="span-idconverting_extended-range_yuv_formatspanspan-idconverting_extended-range_yuv_formatspanspan-idconverting_extended-range_yuv_formatspanconverting-extended-range-yuv-format"></a><span id="Converting_extended-range_YUV_format"></span><span id="converting_extended-range_yuv_format"></span><span id="CONVERTING_EXTENDED-RANGE_YUV_FORMAT"></span>转换扩展范围 YUV 格式


这些图像显示范围从深色到光源的 YUV 范围内内容如何转换（解释为 RGB 格式）：

-   顶部图像显示了错误解释的扩展范围的内容，就像它是工作室范围一样。
-   下图显示了正确解释的扩展范围内容。

顶部图像中的错误解释显示了提高对比度，突出显示在纯白色之前显得非常浅。

![对扩展范围 yuv 内容的错误和正确解释的比较](images/extended-range-yuv.png)

## <a name="span-idextended-range_yuv_interfacespanspan-idextended-range_yuv_interfacespanspan-idextended-range_yuv_interfacespanextended-range-yuv-interface"></a><span id="Extended-range_YUV_interface"></span><span id="extended-range_yuv_interface"></span><span id="EXTENDED-RANGE_YUV_INTERFACE"></span>扩展范围 YUV 接口


在 Windows 8.1 之前，媒体基础仅支持 studio 亮度范围，因此，对扩展范围图像的解释会导致对比度增加，如以上第一个图像中所示。 从 Windows 8.1 开始，媒体基础管道使用这些结构和枚举来指示 Windows 显示驱动程序模型（WDDM）1.3 和更高版本的用户模式显示驱动程序是否正在播放扩展范围或工作室范围 YUV 内容总结

### <a name="span-idnew_enumerationsspanspan-idnew_enumerationsspanspan-idnew_enumerationsspannew-enumerations"></a><span id="New_enumerations"></span><span id="new_enumerations"></span><span id="NEW_ENUMERATIONS"></span>新枚举

-   [**D3D11\_1DDI\_视频\_处理器\_名义\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_nominal_range)
-   [**DXVAHDDDI\_公称\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)

### <a name="span-idchanged_structures_and_enumerationsspanspan-idchanged_structures_and_enumerationsspanspan-idchanged_structures_and_enumerationsspanchanged-structures-and-enumerations"></a><span id="Changed_structures_and_enumerations"></span><span id="changed_structures_and_enumerations"></span><span id="CHANGED_STRUCTURES_AND_ENUMERATIONS"></span>更改的结构和枚举

-   [**D3D11\_1DDI\_视频\_处理器\_颜色\_空间**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11\_1DDI\_视频\_处理器\_设备\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**DXVAHDDDI\_BLT\_状态\_输出\_颜色\_空间\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_blt_state_output_color_space_data)
-   [**DXVAHDDDI\_流\_状态\_输入\_颜色\_空间\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_input_color_space_data)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)

**请注意**  WDDM 1.3 和更高版本的用户模式显示驱动程序必须支持所有这些新的和更改的结构和枚举。

 

有关如何在不同的输入 RGB 和 YUV 格式之间进行转换的详细信息，请参阅[YUV-RGB 数据范围转换](yuv-rgb-data-range-conversions.md)。

 

 





