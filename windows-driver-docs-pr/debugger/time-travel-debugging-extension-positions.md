---
title: 时间行程调试扩展！位置命令
description: ！位置扩展显示所有活动线程，包括它们的当前位置。
keywords:
- 定位 Windows 调试
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04651c8a9c416982720a15b7b3aa2d10bef3396
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916210"
---
# <a name="positions"></a>！位置

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png) 

**！位置**扩展显示所有活动线程，包括其在时间行程跟踪中的当前位置。

```dbgcmd
!positions 
```

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>Parameters

无

## <a name="example"></a>示例

此输出显示四个线程。 线程3824是由左栏中 **>** 指示的当前线程。

```dbgcmd
0:000> !positions
>Thread ID=0x3824 - Position: F:0
 Thread ID=0x2684 - Position: A5:0
 Thread ID=0x2478 - Position: 200:0
 Thread ID=0x2DC4 - Position: 401:0
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

此扩展仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>另请参阅

[行程调试-扩展命令](time-travel-debugging-extension-commands.md)