---
title: 示例6清除所有标志
description: 示例6清除所有标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 002d93698e65bb802a97186039b3767580a45b82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840439"
---
# <a name="example-6-clearing-all-flags"></a>示例6：清除所有标志


## <span id="ddk_example_6___clearing_all_flags_dtools"></span><span id="DDK_EXAMPLE_6___CLEARING_ALL_FLAGS_DTOOLS"></span>


此示例演示了两种不同的方法来清除注册表和会话中设置的所有标志：

-   减去当前标志值。

-   减去高值。

**注意**   此示例演示的方法仅清除标志。 它们不会将 "最大堆栈跟踪大小" 或 "内核特殊池" 标记重置为默认值。

 

### <a name="span-idsubtract_the_current_flag_valuespanspan-idsubtract_the_current_flag_valuespanspan-idsubtract_the_current_flag_valuespansubtract-the-current-flag-value"></a><span id="Subtract_the_Current_Flag_Value"></span><span id="subtract_the_current_flag_value"></span><span id="SUBTRACT_THE_CURRENT_FLAG_VALUE"></span>减去当前标志值

下面的命令通过减去项的当前值，清除注册表中系统范围标记项中设置的所有标志。 在此示例中，当前值为0xE0。 该命令使用 **/r** 参数来指示系统范围内的注册表模式，并使用减号 (-) 来从标志值减去 e0。

```console
gflags /r -E0 
```

在响应中，GFlags 显示系统范围标志注册表项的修订值。 如果值为零，则指示命令成功，且注册表中不再有任何系统范围内的标志设置。

```console
Current Boot Registry Settings are: 00000000 
```

请注意，以下命令与此示例中使用的命令具有相同的效果，并且可以互换使用：

```console
gflags /r -20 -40 -80 
gflags /r -hfc -hpc -hvc 
```

### <a name="span-idsubtract_high_valuesspanspan-idsubtract_high_valuesspanspan-idsubtract_high_valuesspansubtract-high-values"></a><span id="Subtract_High_Values"></span><span id="subtract_high_values"></span><span id="SUBTRACT_HIGH_VALUES"></span>减去高值

下面的命令通过从系统范围标志设置中减去高值 (0xFFFFFFFF) 来清除系统范围内的所有标志。

```console
gflags /r -ffffffff 
```

在响应中，GFlags 显示系统范围标志条目的修订值。 如果值为零，则指示命令成功，且注册表中不再有任何系统范围内的标志设置。

```console
Current Boot Registry Settings are: 00000000 
```

**提示**   在记事本中键入此命令，然后将文件另存为 clearflag.bat。 此后，若要清除所有标志，只需键入 " **ClearFlag**"。

 

最后，下面的示例演示清除所有标志的直观方法不起作用。

以下命令会将系统范围标志条目的值设置为0。 但实际上，它会将零添加到系统范围的标志值。 在此示例中，系统范围标志条目的当前值为0xE0。

```console
gflags /r 0 
```

作为响应，GFlags 在命令完成后显示系统范围内的标志值：

```console
Current Boot Registry Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

此命令不起作用，因为它将值0添加到系统范围的标志条目。

 

 





