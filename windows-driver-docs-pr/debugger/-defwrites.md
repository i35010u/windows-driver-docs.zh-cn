---
title: defwrites
description: Defwrites 扩展显示缓存管理器使用的内核变量的值。
keywords:
- 缓存管理器
- defwrites Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- defwrites
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22b2a272d1960a0284e300a8e4b34b34cc21ef1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814677"
---
# <a name="defwrites"></a>!defwrites


**！ Defwrites** 扩展显示缓存管理器使用的内核变量的值。

```dbgcmd
!defwrites
```

## <span id="ddk__defwrites_dbg"></span><span id="DDK__DEFWRITES_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll
 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关写入阻止功能的信息，请参阅 Russinovich 和 David 的 *Microsoft Windows 内部机制* 。 

有关其他缓存管理扩展的信息，请使用 [**！ cchelp**](-cchelp.md) 扩展。

<a name="remarks"></a>备注
-------

当延迟写入 ( "脏页" ) 变得太大时，将限制页写入。 此扩展允许您查看系统是否已达到此点。

以下是示例：

```dbgcmd
kd> !defwrites 
**_ Cache Write Throttle Analysis _*_

        CcTotalDirtyPages:                   0 (       0 Kb)
        CcDirtyPageThreshold:             1538 (    6152 Kb)
        MmAvailablePages:                 2598 (   10392 Kb)
        MmThrottleTop:                     250 (    1000 Kb)
        MmThrottleBottom:                   30 (     120 Kb)
        MmModifiedPageListHead.Total:      699 (    2796 Kb)

Write throttles not engaged
```

在这种情况下，没有脏页。 如果 _ *CcTotalDirtyPages** 达到 1538 (**CcDirtyPageThreshold**) 的值，则写入将被延迟，直到减少脏页的数目。

 

 





