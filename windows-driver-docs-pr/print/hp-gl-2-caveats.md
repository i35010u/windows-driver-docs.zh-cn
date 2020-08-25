---
title: HP-GL/2 注意事项
description: HP-GL/2 注意事项
ms.assetid: 201a894e-5d22-46f8-965d-0e5b88dc54d7
keywords:
- HP-GL/2 单色 WDK Unidrv，其他注意事项
- PCL-5e WDK Unidrv，其他注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa61d1d813d3db12544d877d9a4a4cb4dc8b835f
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802591"
---
# <a name="hp-gl2-caveats"></a>HP-GL/2 注意事项





1.  HP-UX/2 仅适用于随 Windows XP 及更高版本的操作系统版本一起提供的 Unidrv 版本， (Windows XP Unidrv 是指随 Windows XP 一起提供的驱动程序文件集--unidrv.dll、unidrvui.dll、unires.dll 和 stdnames) gpd。 它在 Windows 2000 Unidrv 上不起作用。 如果运行 Windows 2000 的计算机上存在 Windows XP 版本的 Unidrv (例如，当 Windows 2000 计算机对运行 Windows Server 2003 或更高版本的计算机进行指向和打印连接时) ，则驱动程序将使用 HP-UX/2。

2.  当激活惠普/2 模式时，GPD 中的某些呈现命令会被忽略。 而是使用驱动程序中的硬编码命令。 但是，这些命令必须存在于 GPD 中，原因如下：
    1.  在更高版本的操作系统中，可能会删除呈现命令的硬编码。
    2.  HP-GL/2 驱动程序提供了一个选项，用于切换到光栅模式 (也就是说，不使用 HP-UX/2 驱动程序) 。 对于光栅模式，所有命令都必须存在于 GPD 中。

        很好的经验法则是，任何用于实际绘制某些内容 (例如，CmdDownloadPattern 或 CmdSelectBlackBrush) 的 PCL-XL/HP-UX/2 命令都将被忽略。 不会忽略页面设置、文档设置和其他不是绘制命令的命令。 有关这些命令的详细信息，请参阅 [Color 命令](color-commands.md)。

        另外，驱动程序中的所有 HP-UX/2 命令都是硬编码的。

3.  调用 [**DrvBitBlt**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvbitblt) 和其他位块传输函数时收到的掩码可能无法正常工作。

4.  如果在 Windows 2000 上使用 Windows XP Unidrv 并且激活了 HP-UX/2，则某些图形呈现功能可能无法正常工作。 例如， [**DrvGradientFill**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvgradientfill) 调用的输出具有红色和蓝色反转。

5.  Unidrv 假定打印机硬件支持 ROP 命令。 如果打印机不支持 ROP，则某些文档可能无法正确打印。

6.  需要对影线画笔进行支持。 如果打印机不支持阴影画笔，则输出取决于打印机硬件如何处理 (FT21，x SV21，x) 的阴影画笔选择命令。

7.  单色打印机的阴影画笔颜色会被忽略。 它总是打印为黑色。

8.  对于彩色打印机，HP-GL/2 仅支持 24 bpp/600 dpi。 对于单色打印机，HP-GL/2 仅支持 600 dpi。 如果你的打印机支持其他值，则仅当颜色深度为 24 bpp 并且分辨率为 600 dpi 时，才选择 "仅限 HP-UX/2" 模式。 下面的示例演示如何修改 GraphicsMode 功能以实现此目的。 在此示例中， \* 如果解析功能的选项2值不是 600x600 dpi，则第一个约束条目会导致 Unidrv 拒绝对 HPGL2MODE 的模式更改。 在此示例中 (，假设选项2值为一些较低的分辨率，如 300x300 dpi。 \* 如果 ColorMode 功能的选项是 Color 或8bpp，则第二个约束条目 ) 会导致 Unidrv 拒绝模式更改。
    ```cpp
    *Feature: GraphicsMode
    {
      *rcNameID: =GRAPHICSMODE_DISPLAY
      *FeatureType: DOC_PROPERTY
      *HelpIndex: 12000
      *DefaultOption: HPGL2MODE
      *Option: HPGL2MODE
       {
         *rcNameID: =GRAPHICSMODE_HPGL2_DISPLAY
         *Constraints: Resolution.Option2
         *Constraints: LIST(ColorMode.Color, ColorMode.8bpp)
       }
      *Option: RASTERMODE
       {
         *rcNameID: =GRAPHICSMODE_RASTER_DISPLAY
       }
    }
    ```

9.  彩色打印机必须能够缩放硬件上的图像。 单色打印机不存在此要求。

10. 对于单色打印机，假设：
    -   打印机只接受1bpp 信息。
    -   设置为1的位表示黑色像素，而位设置为0，表示白色像素。
    -   打印机无法以灰色缩放任何颜色。  (这种情况自然是由 1 bpp 限制引起的。 ) 

11. 必须支持以下压缩方法：
    -   无压缩
    -   TIFF
    -   增量行

12. HP-GL/2 不执行系统横向旋转。 启用 "HP-GL/2" 时，会假定打印机处理横向模式下打印的页面的 rasters、字体和坐标。 若要解决此问题，请确保 \* 将 "RotateCoordinate？"、" \* RotateFont" 和 " \* RotateRaster") 属性**TRUE** (的所有 "旋转" 参数设置为 "TRUE"。 如果你的打印机在旋转时出现内存溢出问题，你应考虑不激活惠普/2，或将约束置于内存 (也就是说，仅当内存为 4 MB 或更大时，才应激活 HP-UX/2。

    在低内存设备上 (例如，600 dpi 单色激光打印机，) RAM 为 2 MB，在设备处于 HP-GL/2 模式时，某些页面会出现内存不足错误。 一种解决方案，适用于具有小于完整的内存位图的设备，以便将 GPD 写入到默认值，并让系统处理横向旋转，而不是使用惠普/2。 此外，某些复杂的纵向打印作业可能会在光栅模式下正确打印，但不能在 HP-GL/2 模式下打印。 如果是这种情况，应考虑将光栅模式设为默认值。

13. 在 HP-UX/2 模式下，打印机属性页的 " **高级** " 选项卡上的 "打印优化" 功能当前已被忽略。

14. \*MirrorRasterPage?在 HP-UX/2 模式下不受支持。

15. 即使 GPD 文件指定设备支持轮廓字体，也可以将 TrueType 轮廓字体作为光栅字体下载。 这可能是由于多种原因造成的 (例如，打印机) 上的内存不足。

 

 




