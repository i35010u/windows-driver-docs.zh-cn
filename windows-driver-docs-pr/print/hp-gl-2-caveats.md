---
title: HP-GL/2 注意事项
description: HP-GL/2 注意事项
ms.assetid: 201a894e-5d22-46f8-965d-0e5b88dc54d7
keywords:
- HP/2 单色 WDK Unidrv，其他注意事项
- PCL 5e WDK Unidrv，其他注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394529ca3723c5cf127ec36efb7f1d5fdabef2cc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373811"
---
# <a name="hp-gl2-caveats"></a>HP-GL/2 注意事项





1.  HP/2 仅适用于 Windows xp 附带 Unidrv 和更高版本的操作系统版本 （Windows XP Unidrv 引用随 Windows XP-unidrv.dll、 unidrvui.dll、 unires.dll 和 stdnames.gpd 一起提供的驱动程序文件集） 的版本。 它不会用于 Windows 2000 Unidrv。 如果 （例如，当 Windows 2000 机器进行点并打印连接到计算机运行 Windows Server 2003 或更高版本） 中运行 Windows 2000 的计算机上存在 Unidrv 的 Windows XP 版本，则驱动程序使用 HP/2。

2.  时激活 HP/2 模式，将忽略某些 GPD 中的呈现命令。 相反，使用驱动程序中的硬编码的命令。 但是，这些命令必须位于 GPD 原因如下：
    1.  在更高版本的操作系统，呈现命令进行硬编码可能会删除。
    2.  HP/2 驱动程序提供了一个选项以切换到光栅模式 (即，不使用 HP/2 驱动程序)。 光栅模式的所有命令必须位于 GPD。

        好的经验法则是，用于实际绘制一些内容 （例如，CmdDownloadPattern 或 CmdSelectBlackBrush） 任何 PCL-XL/HP-GL/2 命令将被忽略。 不绘制命令如页面设置、 安装程序文档，以及其他命令不会被忽略。 有关这些命令的详细信息，请参阅[颜色命令](color-commands.md)。

        此外，HP/2 的所有命令都都在驱动程序中硬编码。

3.  在调用中收到的掩码[ **DrvBitBlt** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt) ，其他位块传输函数可能无法正常工作。

4.  当在 Windows 2000 上使用 Windows XP Unidrv 并激活 HP/2 时，某些图形呈现函数可能无法正常工作。 例如，从输出[ **DrvGradientFill** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)调用具有红色和蓝色反转。

5.  Unidrv 假定打印机硬件支持 ROP 命令。 如果打印机不支持 ROP，某些文档可能无法正确打印。

6.  阴影画笔的支持是必需的。 如果打印机不支持阴影画笔，然后输出取决于打印机硬件如何处理阴影画笔选定内容命令 （FT21，x SV21，x）。

7.  对于单色打印机将忽略阴影画笔的颜色。 它始终将打印为黑色。

8.  对于彩色打印机 HP/2 支持只有 24 bpp/600 dpi。 对于单色打印机 HP/2 支持仅 600 dpi。 如果您的打印机支持其他值，限制 HP/2 模式是从选择仅当颜色深度为 24 bpp 和解决方法是 600 dpi。 下面的示例演示如何修改 GraphicsMode 功能来实现此目的。 在此示例中，第一个\*约束条目会导致 Unidrv 要拒绝模式更改为 HPGL2MODE 解析功能的选项 2 值是否不 600 x 600 dpi。 （在示例中，假定 Option2 值是某些较低的分辨率，例如 300 x 300 dpi。）第二个\*约束条目会导致 Unidrv 如果 ColorMode 功能的选项为颜色或 8bpp 拒绝模式更改。
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

9.  彩色打印机必须能在硬件上的缩放图像。 单色打印机不存在此要求。

10. 对于单色打印机，假定：
    -   打印机接受仅 1bpp 信息。
    -   位设置为 1 表示黑色像素，位设置为 0 表示白色像素。
    -   打印机无法灰色缩放任何颜色。 （这是由于而导致自然 1 bpp 限制。）

11. 必须支持以下压缩方法：
    -   不进行压缩
    -   TIFF
    -   增量行

12. HP/2 不会执行系统横向旋转。 启用 HP/2，则假定打印机处理光栅图、 字体和在横向模式下打印总页数的坐标的旋转。 若要避免此问题，请确保所有 GPD 旋转参数 ( \*RotateCoordinate？， \*RotateFont？，并\*RotateRaster？ 属性) 设置为**TRUE**。 如果打印机配有旋转内存溢出问题，应考虑不激活 HP-GL/2，或者将它们放置约束内存 （即，HP/2 应激活仅当内存为 4 MB 或更多。

    内存不足的设备 （例如，600 dpi 单色激光打印机使用 2 MB 的 RAM），在某些设备在 HP/2 模式下时生成内存不足错误的页可能光栅模式中正确打印。 适用于设备的一种解决方案，与完整位图小于是内存的编写 GPD，这样该光栅模式是内存的默认值，并让系统处理横向旋转，而不是内存的 HP/2。 此外，某些复杂纵向打印作业可能正确打印在光栅模式下，但不是在 HP/2 模式。 如果是这样，则应考虑将光栅模式设为默认。

13. 在上打印的优化功能**高级**在 HP/2 模式当前被忽略的打印机属性页的选项卡。

14. \*MirrorRasterPage？不支持在 HP/2 模式下。

15. 很可能 TrueType 轮廓字体，因为即使 GPD 文件指定设备支持光栅字体轮廓字体下载。 这可能由于各种原因 （例如，打印机上没有足够内存）。

 

 




