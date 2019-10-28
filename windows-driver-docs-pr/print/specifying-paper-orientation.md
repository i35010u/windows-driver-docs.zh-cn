---
title: 指定纸张方向
description: 指定纸张方向
ms.assetid: 2d62e1ff-965b-4fd7-922c-319ec1bc39a5
keywords:
- Unidrv，纸张方向
- 纸张方向 WDK Unidrv
- 纵向 WDK Unidrv
- LANDSCAPE_CC90 方向 WDK Unidrv
- LANDSCAPE_CC270 方向 WDK Unidrv
- 横向模式 WDK Unidrv
- 纵向模式 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a3898d4ca7022c15765025dfcbf8bad60c1c60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840408"
---
# <a name="specifying-paper-orientation"></a>指定纸张方向





"方向[标准" 功能](standard-features.md)有三个[标准选项](standard-options.md)：纵向、横向\_CC90 和横向\_CC270。 除非另外指定，否则默认方向为纵向。 此选项的使用非常简单，本主题不会进一步讨论。 本主题的平衡涉及两个横向选项。

### <a href="" id="landscape-cc90-and-landscape-cc270"></a>横向\_CC90 和横向\_CC270

"方向" 功能的横向\_CC90 和横向\_CC270 选项指示要应用于纵向模式下的文本和图形的旋转量，以将其转换为横向模式。 横向\_CC90 选项将顺时针旋转文本和图形90度。 横向\_CC270 选项将顺时针旋转文本和图形270度，这相当于顺时针旋转90度。 对于这两个选项，Unidrv 将处理旋转文本和图形的任务，并将其作为新方向适当地移动。

许多打印机支持纵向模式和横向模式，而其余打印机（通常具有较少功能）仅支持纵向模式。 每个模式都有其自己的坐标系统：在纵向模式下，原点位于左上角（x 向右增加，y 向下增加）;在横向模式下，原点位于左下角（x 增加，y 向右增加）。

对于不支持横向模式的打印机，仍可在此方向上打印文档。 对于这种类型的打印机，必须在打印机的 GPD 文件中指定横向\_CC270 选项。 （如果为这些打印机指定了横向\_CC90 选项，则在打印时，文本和图形将显示为乱码。）在此选项下，Unidrv 会将已转换的文本和图形与打印机的左上角原点相对坐标显示给打印机。

对于支持横向模式的打印机以及纵向模式，应在 GPD 文件中指定横向\_CC90 选项。 在此选项下，必须将 Unidrv 定向到打印机的 "向打印机发出横向的命令字符串"，使其从纵向模式坐标系统切换到横向模式坐标系统（原点位于左下角）。 然后，Unidrv 将转换后的文本和图形显示到打印机，其相对于打印机左下角的坐标。

但是，支持横向模式的打印机（通常会使用横向\_CC90 选项），仍可使用横向\_CC270 选项进行操作。 在此选项下，Unidrv 会被定向到将打印机视为仅支持纵向模式（即，只有单个坐标系统，原点位于左上角）。 因此，不能将 Unidrv 定向为发出用于更改坐标系统的命令。 Unidrv 以相对于此左上角原点的坐标向打印机显示已转换的文本和图形。 由于 Unidrv 假定此位置为源位置，因此即使用户在打印机的属性页上选择了横向方向，也不能将此类打印机颁发为横向模式命令字符串。 请注意，在以下 GPD 文件示例中，\*选项：横向\_CC270 部分包含一个命令，用于将打印机置于纵向模式（\_\_纵向），而不是将其置于横向模式。

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

**注意**   适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有用于横向旋转的新参数。 有关详细信息，请参阅[**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

 

 




