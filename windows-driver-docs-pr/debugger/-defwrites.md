---
title: defwrites
description: Defwrites 扩展显示缓存管理器使用的内核变量的值。
ms.assetid: da576e05-3d9f-4599-bf8e-b1fa05093d77
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
ms.openlocfilehash: 2e54cc4f1f01e091870c9979cc77fcaaa2bec9e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562843"
---
# <a name="defwrites"></a>!defwrites


**！ Defwrites**扩展显示的缓存管理器使用的内核变量的值。

```dbgcmd
!defwrites
```

## <span id="ddk__defwrites_dbg"></span><span id="DDK__DEFWRITES_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关写入限制的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

有关其他缓存管理扩展的信息，请使用[ **！ cchelp** ](-cchelp.md)扩展。

<a name="remarks"></a>备注
-------

当延迟写入 （"脏页"） 的次数变得过大时，页写入将受到限制。 该扩展允许您查看您的系统是否已达到此点。

下面是一个示例：

```dbgcmd
kd> !defwrites 
*** Cache Write Throttle Analysis ***

        CcTotalDirtyPages:                   0 (       0 Kb)
        CcDirtyPageThreshold:             1538 (    6152 Kb)
        MmAvailablePages:                 2598 (   10392 Kb)
        MmThrottleTop:                     250 (    1000 Kb)
        MmThrottleBottom:                   30 (     120 Kb)
        MmModifiedPageListHead.Total:      699 (    2796 Kb)

Write throttles not engaged
```

在这种情况下，没有任何脏页。 如果**CcTotalDirtyPages**达到 1538年 (的值**CcDirtyPageThreshold**)，将延迟写入，到脏页的数量会减少。

 

 





