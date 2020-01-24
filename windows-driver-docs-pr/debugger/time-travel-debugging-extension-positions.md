---
title: 时间行程调试扩展！位置命令
description: ！位置扩展显示所有活动线程，包括它们的当前位置。
keywords:
- 定位 Windows 调试
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8e93a42646d0fb6c22901607f3dba4eed0a692ed
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706968"
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

此输出显示5个线程。 线程1660是由左栏中 **>** 指示的当前线程。

```dbgcmd
0:000> !positions
>*Thread ID=0x1660 - Position: 724:0
  Thread ID=0x3E6C - Position: A8B:0
  Thread ID=0x30EC - Position: A8A:0
  Thread ID=0x1F40 - Position: A8E:0
  Thread ID=0x4170 - Position: C44:0
* indicates an actively running thread
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

此扩展仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>另请参阅

[行程调试-扩展命令](time-travel-debugging-extension-commands.md)