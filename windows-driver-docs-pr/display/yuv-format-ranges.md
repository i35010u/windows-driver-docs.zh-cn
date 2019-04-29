---
title: 在 Windows 8.1 的 YUV 格式范围
ms.assetid: D76FFB8C-CA42-446E-826F-52982B1849E5
description: 用户模式显示驱动程序如何利用 YUV 视频格式
keywords:
- 完整范围 YUV WDK 显示
- 扩展范围 YUV WDK 显示
- studio 亮度范围 YUV WDK 显示
- YUV 格式和 WMF 支持 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df9b36283db5b7c8c811ed12ae05a5d0da2ba880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371414"
---
# <a name="yuv-format-ranges-in-windows81"></a>在 Windows 8.1 的 YUV 格式范围


应用程序可以发出信号用户模式显示驱动程序以利用扩展范围\[0，255\] YUV 视频格式从 Windows 8.1，此表中所示：

| YUV 范围                | 输入的数据范围 | 典型用法                                           | 标准                                                  |
|--------------------------|------------------|---------------------------------------------------------|-----------------------------------------------------------|
| *扩展的范围*         | \[0, 255\]       | 使用者设备： 网络摄像头和傻瓜式相机 | 标准版、 JFIF 和 MJPEG 的视频格式将用作默认值 |
| *studio 亮度范围* | \[16, 235\]      | 专业照相机和视频设备                | ITU BT.601 和 BT.709                                     |

 

在更大范围由单个使用者生成的视频时，生成的内容和广播行业的大多数视频是 studio 范围内。 扩展的范围也称为*完整的亮度范围*。

在 Windows 8.1，视频处理管道所作用于所有输入数据，像在 studio 范围内，Microsoft 媒体基础之前这会导致减少动态范围和通常 harsh 对比度如果输入的数据实际在更大范围。

从 Windows 8.1 中扩展范围视频输入的 YUV 格式时，应用可以通知此更高版本的动态范围的驱动程序。

## <a name="span-idconvertingextended-rangeyuvformatspanspan-idconvertingextended-rangeyuvformatspanspan-idconvertingextended-rangeyuvformatspanconverting-extended-range-yuv-format"></a><span id="Converting_extended-range_YUV_format"></span><span id="converting_extended-range_yuv_format"></span><span id="CONVERTING_EXTENDED-RANGE_YUV_FORMAT"></span>将扩展范围 YUV 格式转换


这些图显示如何转换为浅值范围从深的 YUV 扩展范围内容 （解释型） 为 RGB 格式：

-   顶部图像显示不正确地解释扩展范围内容，就好像 studio 范围。
-   下图显示了正确解释扩展范围内容。

在上图中未得到正确解释显示更高的对比度并突出显示变得太亮之前达到纯白色。

![扩展范围 yuv 内容的错误用法和正确解释的比较](images/extended-range-yuv.png)

## <a name="span-idextended-rangeyuvinterfacespanspan-idextended-rangeyuvinterfacespanspan-idextended-rangeyuvinterfacespanextended-range-yuv-interface"></a><span id="Extended-range_YUV_interface"></span><span id="extended-range_yuv_interface"></span><span id="EXTENDED-RANGE_YUV_INTERFACE"></span>扩展范围 YUV 接口


Windows 8.1、 Media Foundation 仅支持 studio 亮度范围之前，因此解释扩展范围图像时增加与之相反，如上面的第一个图像中所示。 从 Windows 8.1 开始，媒体基础管道使用这些结构和枚举，以指示 Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序是否扩展范围或正在播放 studio 范围 YUV 内容或捕获：

### <a name="span-idnewenumerationsspanspan-idnewenumerationsspanspan-idnewenumerationsspannew-enumerations"></a><span id="New_enumerations"></span><span id="new_enumerations"></span><span id="NEW_ENUMERATIONS"></span>新枚举

-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_NOMINAL\_RANGE**](https://msdn.microsoft.com/library/windows/hardware/dn265173)
-   [**DXVAHDDDI\_NOMINAL\_RANGE**](https://msdn.microsoft.com/library/windows/hardware/dn265432)

### <a name="span-idchangedstructuresandenumerationsspanspan-idchangedstructuresandenumerationsspanspan-idchangedstructuresandenumerationsspanchanged-structures-and-enumerations"></a><span id="Changed_structures_and_enumerations"></span><span id="changed_structures_and_enumerations"></span><span id="CHANGED_STRUCTURES_AND_ENUMERATIONS"></span>已更改的结构和枚举

-   [**D3D11\_1DDI\_视频\_处理器\_颜色\_空间**](https://msdn.microsoft.com/library/windows/hardware/hh450970)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_DEVICE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450978)
-   [**DXVAHDDDI\_BLT\_STATE\_OUTPUT\_COLOR\_SPACE\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff563002)
-   [**DXVAHDDDI\_STREAM\_STATE\_INPUT\_COLOR\_SPACE\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff563084)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff563113)

**请注意**  WDDM 1.3 和更高版本的用户模式显示驱动程序必须支持所有这些新功能和更改结构和枚举。

 

请参阅[YUV RGB 数据范围转换](yuv-rgb-data-range-conversions.md)了解不同的输入的 RGB 和 YUV 之间进行转换的详细信息设置的格式。

 

 





