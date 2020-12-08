---
title: 指定纸张方向
description: 指定纸张方向
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
ms.openlocfilehash: e69d8995f42e1d539566eba6769c720e31c6acdc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806891"
---
# <a name="specifying-paper-orientation"></a>指定纸张方向





"方向[标准" 功能](standard-features.md)有三个[标准选项](standard-options.md)：纵向、横向 \_ CC90 和横向 \_ CC270。 除非另外指定，否则默认方向为纵向。 此选项的使用非常简单，本主题不会进一步讨论。 本主题的平衡涉及两个横向选项。

### <a name="landscape_cc90-and-landscape_cc270"></a><a href="" id="landscape-cc90-and-landscape-cc270"></a>横向 \_ CC90 和横向 \_ CC270

\_"方向" 功能的 "横向 CC90" 和 "横向" \_ CC270 选项指示要应用于纵向模式下的文本和图形的旋转量，以将其转换为横向模式。 横向 \_ CC90 选项按逆时针旋转文本和图形90度。 横向 \_ CC270 选项将逆时针旋转文本和图形270度，这相当于顺时针旋转90度。 对于这两个选项，Unidrv 将处理旋转文本和图形的任务，并将其作为新方向适当地移动。

许多打印机支持纵向模式和横向模式，而其余打印机（通常具有较少功能）仅支持纵向模式。 每个模式都有其自己的坐标系统：在纵向模式下，原点位于左上角 (x 向右增加，y 向下增加) ;在横向模式下，原点位于左下角， (x 增加，并将 y 向右) 增加。

对于不支持横向模式的打印机，仍可在此方向上打印文档。 对于这种类型的打印机，必须 \_ 在打印机的 GPD 文件中指定横向 CC270 选项。  (如果您 \_ 为这些打印机指定了横向 CC90 选项，则在打印时文本和图形将显示为乱码。 ) 在此选项下，Unidrv 会将转换的文本和图形显示为相对于打印机左上角原点的坐标。

对于支持横向模式的打印机以及纵向模式，应 \_ 在 GPD 文件中指定横向 CC90 选项。 在此选项下，必须将 Unidrv 定向到打印机上的 "向打印机发出横向命令字符串"，使其从纵向模式坐标系统切换到 "横向模式" 协调系统 () 左下角的原点。 然后，Unidrv 将转换后的文本和图形显示到打印机，其相对于打印机左下角的坐标。

但是，支持横向模式 (的打印机通常会在 \_) 使用横向 CC90 选项，但仍可使用 \_ CC270 选项进行操作。 在此选项下，Unidrv 会被定向到将打印机视为仅支持纵向模式 (也就是说，只有单个坐标系统，原点位于左上角) 。 因此，不能将 Unidrv 定向为发出用于更改坐标系统的命令。 Unidrv 以相对于此左上角原点的坐标向打印机显示已转换的文本和图形。 由于 Unidrv 假定此位置为源位置，因此即使用户在打印机的属性页上选择了横向方向，也不能将此类打印机颁发为横向模式命令字符串。 在下面的 GPD 文件示例中，请注意 \* 选项：横向 \_ CC270 部分包含一个命令，用于将打印机置于纵向模式 (定向到 \_ 纵向 \_ CMD) ，而不是将其置于横向模式。

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

**注意**   对于 Windows 7， **MxdcGetPDEVAdjustment** 函数具有用于横向旋转的新参数。 有关详细信息，请参阅 [**MxdcXDCGetPDEVAdjustment**](/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

 

