---
title: 示例 6 清除所有标志
description: 示例 6 清除所有标志
ms.assetid: 07a6af3d-3ef7-429d-9afa-439b20915ab1
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d76940e358f53d82f4785332849140710e0316d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521879"
---
# <a name="example-6-clearing-all-flags"></a>示例 6:清除所有标志


## <span id="ddk_example_6___clearing_all_flags_dtools"></span><span id="DDK_EXAMPLE_6___CLEARING_ALL_FLAGS_DTOOLS"></span>


此示例演示两种不同方法来清除所有标志在注册表和会话设置：

-   减去当前的标志值。

-   减去较高的值。

**请注意**  仅标记此示例清晰演示的方法。 它们不做为默认值重置最大堆栈跟踪大小或内核特殊池标记。

 

### <a name="span-idsubtractthecurrentflagvaluespanspan-idsubtractthecurrentflagvaluespanspan-idsubtractthecurrentflagvaluespansubtract-the-current-flag-value"></a><span id="Subtract_the_Current_Flag_Value"></span><span id="subtract_the_current_flag_value"></span><span id="SUBTRACT_THE_CURRENT_FLAG_VALUE"></span>当前的标志值减去

以下命令清除减去当前条目的值设置在注册表中系统级标志条目中的所有标志。 在此示例中，当前值是 0xE0。 该命令使用 **/r**参数以指示整个系统注册表模式和带有减号 （-） 从标志值减去 E0 E0 值。

```console
gflags /r -E0 
```

在响应中，用 GFlags 显示系统范围内标志注册表项的修订的值。 零值指示该命令成功，而且将不再在注册表中的任何系统范围内标志集。

```console
Current Boot Registry Settings are: 00000000 
```

请注意，以下命令具有相同的效果与在此示例中所使用的命令可以互换使用：

```console
gflags /r -20 -40 -80 
gflags /r -hfc -hpc -hvc 
```

### <a name="span-idsubtracthighvaluesspanspan-idsubtracthighvaluesspanspan-idsubtracthighvaluesspansubtract-high-values"></a><span id="Subtract_High_Values"></span><span id="subtract_high_values"></span><span id="SUBTRACT_HIGH_VALUES"></span>将高值相减

以下命令清除较高的值 (0xFFFFFFFF) 减去的系统范围内标志设置的所有系统级标志。

```console
gflags /r -ffffffff 
```

在响应中，用 GFlags 显示系统范围内标志条目的修订的值。 零值指示该命令成功，而且将不再在注册表中的任何系统范围内标志集。

```console
Current Boot Registry Settings are: 00000000 
```

**提示**  到记事本中，键入以下命令，然后将文件另存 clearflag.bat。 此后，若要清除所有标志，只需键入**ClearFlag**。

 

最后，下面的示例演示，清除所有标志的直观方法不会不起作用。

以下命令将显示系统范围内标志条目的值设置为 0。 但是，它实际上添加零到整个系统的标志值。 在此示例中，整个系统标记项的当前值是 0xE0。

```console
gflags /r 0 
```

在响应中，GFlags 显示整个系统的标志值，该命令完成后：

```console
Current Boot Registry Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

该命令没有任何作用，因为它将值 0 添加到系统范围内标志条目。

 

 





