---
title: 时间旅行调试扩展 ！ 定位命令
description: ！ 扩展插件都会显示所有活动的线程，包括其当前的位置的位置。
keywords:
- 定位 Windows 调试
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 036d7057fefec0a39780ddad259079c81ac73605
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568135"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="positions"></a>！ 位置


**！ 位置**扩展插件都会显示所有活动的线程，包括其时间旅行跟踪中的当前位置。


```dbgcmd
!positions 
```


## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>参数

无


## <a name="example"></a>示例

此输出显示了四个线程。 线程 3824 是由当前线程**>** 左侧列中。

```dbgcmd
0:000> !positions
>Thread ID=0x3824 - Position: F:0
 Thread ID=0x2684 - Position: A5:0
 Thread ID=0x2478 - Position: 200:0
 Thread ID=0x2DC4 - Position: 401:0
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展只适用于时间传输跟踪。 有关按时间顺序查看详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


## <a name="see-also"></a>请参阅

[时间旅行调试-扩展的命令](time-travel-debugging-extension-commands.md)


 

 





