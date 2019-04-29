---
title: 时间旅行调试扩展 ！ tt 命令
description: ！ Tt 时间旅行调试器扩展，可用于在时间中向前和向后导航。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26817ac6f106064afdec8f80a74359c23d476768
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389119"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

#  <a name="tt-time-travel"></a>！ tt （时程）

！ Tt （时程） 调试器扩展，可用于在时间中向前和向后导航。

## <a name="tt-navigation-commands"></a>！ tt 导航命令

使用 ！ tt 扩展向前或向后导航通过体验到在跟踪中的给定位置中的时间。 

```dbgcmd
!tt [position] 
```

## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>参数

**position**

提供在任何时间传输到该点的以下格式的时间位置。
           
- 如果 {位置} 是介于 0 和 100 之间的十进制数字，它跟踪到传输大约该 %。 例如：
    - ！ ttdext.tt 0-时间旅行到跟踪的开头
    - ！ ttdext.tt 50-时间出差到一半通过跟踪
    - ！ ttdext.tt 到跟踪的末尾 100-按时间顺序查看
 

- 如果 {位置} #: #，其中 # 为十六进制数字，它传递到该位置。 如果数字格式后： 已省略，默认为零。
    - ！ ttdext.tt 1A0:-按照时间顺序逐个来定位 1A0:0
    - ！ ttdext.tt 1A0:0-来定位 1A0:0 按时间顺序查看
    - ！ ttdext.tt 1A0:12F-来定位 1A0:12F 按时间顺序查看


   > [!NOTE]
   > 跟踪使用的两部分指令位置引用在跟踪中的特定位置引用，例如 12:0。 或 15:7。 两个元素是十六进制数字定义如下所述。
   >
   > xx:yy
   > 
   > xx 的第一个元素是序列化数，它对应于序列化事件。
   >
   > yy-第二个元素是步骤计数，与对应的大致指令计数因为序列化事件。


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

此扩展只适用于时间传输跟踪。 有关按时间顺序查看详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---






