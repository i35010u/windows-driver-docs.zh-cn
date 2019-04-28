---
title: 时间旅行导航命令
description: 本部分介绍时间旅行导航命令。
ms.date: 09/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b07f9dbc2b5f447ad6229fd6782ed0d3e019bb9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349029"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png)

# <a name="time-travel-navigation-commands"></a>时间旅行导航命令

本部分介绍时间旅行导航命令。


## <a name="spanspan-idpspan-p--step-back"></a></span><span id="P"></span> p-（后退）

*P-* 命令执行前面的单个指令或源行。 当子例程调用或中断发生，它们被视为单步执行。 您可以调用此命令使用**单步通过后退**按钮**主页**WinDbg 预览版中的功能区。
 

## <a name="spanspan-idtspan-t--trace-back"></a></span><span id="T"></span> t-（回溯）

*T-* 命令执行前面的单个指令或源行。 当出现子例程调用或中断，也将他们执行的步骤的每个被跟踪。 您可以调用此命令使用**单步到后退**按钮**主页**WinDbg 预览版中的功能区。


## <a name="spanspan-idgospan-g--go-back"></a></span><span id="Go"></span> g-（返回）

*G-* 命令将启动当前进程执行相反的顺序。 BreakAddress 命中时，或另一个事件导致调试器停止时，执行将暂停程序，结尾处。 您可以调用此命令使用**转到后退**按钮**主页**WinDbg 预览版中的功能区。


## <a name="spanspan-idadditionalinformationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

旅行导航命令仅处理时间的时间传输跟踪。 有关按时间顺序查看详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

[时间旅行调试-重播的跟踪](time-travel-debugging-replay.md)

---






