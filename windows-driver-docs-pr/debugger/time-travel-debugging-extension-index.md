---
title: 时间旅行调试扩展 ！ 索引命令
description: ！ 索引扩展索引按时间顺序查看跟踪或显示索引的状态信息。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e5b6875e29a47074688c39d1398e121607f107aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542849"
---
#  <a name="index"></a>!index

![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

**！ 索引**扩展索引按时间顺序查看跟踪或显示索引的状态信息。

```dbgsyntax
!index [-status] [-force] 
```


使用`!index`通过当前的跟踪运行的索引传递。 

```dbgcmd
0:000> !index
Indexed 10/14 keyframes
Indexed 14/14 keyframes
Successfully created the index in 535ms.
```

如果当前跟踪已编制索引，！ 索引命令不执行任何操作。

```dbgcmd
0:000> !index
Successfully created the index in 0ms.
```



## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>参数

**-status**

使用`!index -status`报告跟踪索引的状态。

```dbgcmd
0:000> !tt.index -status
Index file loaded.
```
**-force**

使用`!index -force`即使磁盘上存在无法加载索引文件，跟踪重新编制索引。

```dbgcmd
0:000> !tt.index -force
Successfully created the index in 152ms.
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展只适用于时间传输跟踪。 有关按时间顺序查看详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


## <a name="see-also"></a>另请参阅

[时间旅行调试-扩展的命令](time-travel-debugging-extension-commands.md)


-------

 





