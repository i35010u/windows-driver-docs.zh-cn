---
title: 时间行程调试扩展！ tt 命令
description: 允许您在时间中向前和向后导航的！ tt 时间旅行调试器扩展。
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6af058ee25e25ee1875beb3a94005d526f895860
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706945"
---
# <a name="tt-time-travel"></a>！ tt （行程）

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

允许您在时间中向前和向后导航的！ tt （时间段）调试器扩展。

## <a name="tt-navigation-commands"></a>！ tt 导航命令

使用！ tt 扩展，通过前往跟踪中的给定位置，向前或向后导航。 

```dbgcmd
!tt [position]
```

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>Parameters

**position**

提供以下任意格式的时间位置以在该时间点旅行。
           
- 如果 {position} 是一个介于0到100之间的十进制数字，则它会在跟踪中大约向其传递百分比。 例如：
    - ！ tt 0-到跟踪开头的时间
    - ！ tt 50-时间通过跟踪的一半时间
    - ！ tt 100-时间到达跟踪结尾
 

- 如果 {position} 为 #： #，其中 # 是十六进制数字，则将其移动到该位置。 如果省略了 after：，则默认为零。
    - ！ tt 1A0：-Time 旅行到1A0：0
    - ！ tt 1A0： 0-时间走到位置1A0：0
    - ！ tt 1A0：12F 旅行到位置1A0：12F


   > [!NOTE]
   > 跟踪使用两部分说明位置，该位置引用跟踪中的特定位置引用，例如12:0。 或15:7。 这两个元素是按此处所述定义的十六进制数。
   >
   > xx： yy
   > 
   > xx-第一个元素是对应于序列化事件的序列号。
   >
   > yy-第二个元素是一个步骤计数，它大致对应于自排序事件之后的指令计数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

此扩展仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)
