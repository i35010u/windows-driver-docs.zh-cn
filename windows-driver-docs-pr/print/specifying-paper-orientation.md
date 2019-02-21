---
title: 指定纸张方向
description: 指定纸张方向
ms.assetid: 2d62e1ff-965b-4fd7-922c-319ec1bc39a5
keywords:
- Unidrv，纸张方向
- 纸张方向 WDK Unidrv
- 纵向方向 WDK Unidrv
- LANDSCAPE_CC90 方向 WDK Unidrv
- LANDSCAPE_CC270 方向 WDK Unidrv
- 横向模式 WDK Unidrv
- 纵向模式 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 428bfa4c9bd84cd2981e09362e813df5dbb78c99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543606"
---
# <a name="specifying-paper-orientation"></a>指定纸张方向





有三个[标准选项](standard-options.md)方向与相关联[标准功能](standard-features.md):PORTRAIT、 LANDSCAPE\_CC90 和横向\_CC270。 除非另行指定，默认方向为纵向。 使用此选项很简单，并且不再进一步讨论此主题中。 本主题的平衡涉及到两个布局选项。

### <a href="" id="landscape-cc90-and-landscape-cc270"></a>横向\_CC90 和横向\_CC270

横向\_CC90 和横向\_CC270 选项的方向功能指示要应用于文本和图形在纵向模式下，将它们转换为横向模式的旋转量。 横向\_CC90 选项将文本和图形逆时针旋转 90 度。 横向\_CC270 选项将文本和图形 270 逆时针旋转度，这等同于旋转顺时针旋转 90 度的旋转。 有关这两个选项，Unidrv 处理旋转的文本和图形所指示的量，然后将它们移根据新方向的任务。

许多打印机支持纵向模式和横向模式，而剩下的打印机，通常为那些具有较少的功能，仅支持纵向模式。 每个模式具有其自己的坐标系统： 在纵向模式中，原点位于左上角 (x 增加向右和向下 y 增加）;在横向模式中，原点位于左下角 (x 增加向上和向右 y 增加）。

不支持横向模式下的打印机仍可在此方向打印文档。 对于此类型的打印机，您必须指定横向\_CC270 打印机的 GPD 文件中的选项。 (如果指定横向\_打印时，这些打印机、 文本和图形的 CC90 选项将显示出现乱码。)此选项下, Unidrv 坐标相对于打印机的上限左上角原点中显示的已转换的文本和图形到打印机。

对支持横向模式和纵向模式的打印机，应指定横向\_CC90 GPD 文件中的选项。 此选项下 Unidrv 必须定向将布局命令字符串发送到打印机，使其从纵向模式坐标系统切换到横向模式下坐标系统 （使用左下角处的原点）。 Unidrv 然后向呈现的已转换的文本和图形转换为打印机坐标相对于打印机的较低左上角原点。

但是，支持的打印机横向模式 (为其横向\_通常会使用 CC90 选项)，仍可以运行使用横向打印\_CC270 选项。 此选项下 Unidrv 重定向，以将打印机视为支持仅纵向模式 (即，只有单个坐标系统中，使用左上角处的原点)。 因此，Unidrv，未必须定向发出命令来更改坐标系统。 Unidrv 坐标相对于此上限左上角原点中提供的已转换的文本和图形到打印机。 由于 Unidrv 假定原点的此位置，此类打印机必须不颁发横向模式命令字符串，即使用户所选打印机的属性页上的布局方向。 在下面的 GPD 文件示例，请注意，\*选项：横向\_CC270 部分包含要使打印机处于纵向模式的命令 (面向\_纵向\_CMD)，而不是以将其放入横向模式。

```cpp
*Feature: Orientation
{
  *rcNameID: =ORIENTATION_DISPLAY
  *DefaultOption: PORTRAIT
  *Option: PORTRAIT
  {
    *rcNameID: =PORTRAIT_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.60
      *Cmd: =ORIENT_PORTRAIT_CMD
    }
  }
  *Option: LANDSCAPE_CC270
   {
     *rcNameID: =LANDSCAPE_DISPLAY
     *Command: CmdSelect
     {
       *Order: DOC_SETUP.60
       *Cmd: =ORIENT_PORTRAIT_CMD
     }
  }
}
```

**请注意**  适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有横向旋转的新参数。 有关详细信息，请参阅[ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)。

 

 

 




