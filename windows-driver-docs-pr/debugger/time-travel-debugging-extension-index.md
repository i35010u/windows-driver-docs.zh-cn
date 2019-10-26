---
title: 时间行程调试扩展！索引命令
description: ！索引扩展索引时间段跟踪或显示索引状态信息。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 044410ba9e7ac93c2f27c589a8f30bfb00d95d9a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916213"
---
#  <a name="index"></a>！索引

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

**！索引**扩展索引时间段跟踪或显示索引状态信息。

```dbgsyntax
!index [-status] [-force] 
```


使用 `!index` 对当前跟踪运行索引传递。 

```dbgcmd
0:000> !index
Indexed 10/14 keyframes
Indexed 14/14 keyframes
Successfully created the index in 535ms.
```

如果当前跟踪已建立索引，则！ index 命令不执行任何操作。

```dbgcmd
0:000> !index
Successfully created the index in 0ms.
```



## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>Parameters

**-status**

使用 `!index -status` 报告跟踪索引的状态。

```dbgcmd
0:000> !tt.index -status
Index file loaded.
```
**-force**

即使磁盘上存在无法加载的索引文件，也可以使用 `!index -force` 来重新索引跟踪。

```dbgcmd
0:000> !tt.index -force
Successfully created the index in 152ms.
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

此扩展仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>另请参阅

[行程调试-扩展命令](time-travel-debugging-extension-commands.md)
