---
title: 旅行导航命令
description: 本部分介绍了旅行导航命令。
ms.date: 09/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb47543b30234a31feff4e9bafc1ed929cb3775
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916192"
---
# <a name="time-travel-navigation-commands"></a>旅行导航命令

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png)

本部分介绍了旅行导航命令。

## <a name="spanspan-idpspan-p--step-back"></a></span><span id="P"></span> p-（逐步返回）

*P*命令执行上一条指令或源行。 当发生子程序调用或中断时，它们将被视为单个步骤。 可以使用 WinDbg Preview 中**Home**功能区上的 "**逐过程**" 按钮调用此命令。

## <a name="spanspan-idtspan-t--trace-back"></a></span><span id="T"></span> t-（Trace Back）

*T*命令执行上一条指令或源行。 当发生子程序调用或中断时，也会跟踪其每个步骤。 可以使用 WinDbg Preview 中**Home**功能区上的 "**单步执行**" 按钮调用此命令。

## <a name="spanspan-idgospan-g--go-back"></a></span><span id="Go"></span> g-（返回）

*G*命令开始反向执行当前进程。 当命中 BreakAddress 或其他事件导致调试器停止时，执行将在程序结束时停止。 可以使用 WinDbg Preview 中**Home**功能区上**的 "返回**" 按钮调用此命令。

## <a name="spanspan-idadditional_informationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

旅行导航命令仅适用于时间行程跟踪。 有关时间段的详细信息，请参阅[行程调试-概述](time-travel-debugging-overview.md)。

## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)

[旅行调试-重播跟踪](time-travel-debugging-replay.md)
