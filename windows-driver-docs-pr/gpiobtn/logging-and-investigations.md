---
title: 日志记录和调查
description: 本主题介绍日志记录和调查的 GPIO 实现。
ms.assetid: 27D6349D-5F92-450B-B9AA-90BA9C5D7E65
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60b92bcd702c6d59c12a8473c23372540e1c8dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392627"
---
# <a name="logging-and-investigations"></a>日志记录和调查


本主题介绍日志记录和调查的 GPIO 实现。

## <a name="span-idlivedebugprintsfromthekerneldebuggerspanspan-idlivedebugprintsfromthekerneldebuggerspanspan-idlivedebugprintsfromthekerneldebuggerspanlive-debug-prints-from-the-kernel-debugger"></a><span id="Live_debug_prints_from_the_kernel_debugger"></span><span id="live_debug_prints_from_the_kernel_debugger"></span><span id="LIVE_DEBUG_PRINTS_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试程序的实时调试打印


``` syntax
!wmitrace.start buttonTrace -kd ; !wmitrace.enable buttonTrace {5a81715a-84c0-4def-ae38-edde40df5b3a} -level 4 -flag 0xFFFFFFFF
<repro>
!wmitrace.stop buttonTrace
```

## <a name="span-idlogsandinvestigationsspanspan-idlogsandinvestigationsspanspan-idlogsandinvestigationsspanlogs-and-investigations"></a><span id="Logs_and_investigations"></span><span id="logs_and_investigations"></span><span id="LOGS_AND_INVESTIGATIONS"></span>日志和调查


从 KD IFR 日志：

``` syntax
!rcdrkd msgpiowin32 
```

LogMan:

``` syntax
 
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>
logman stop -ets buttonTrace
```

### <a name="span-idvalidationsspanspan-idvalidationsspanspan-idvalidationsspanvalidations"></a><span id="Validations"></span><span id="validations"></span><span id="VALIDATIONS"></span>验证

可以使用 IFR 日志或 Logman 验证正确切换状态。

例如，如果希望停靠指示器更改，以下条目应是日志中找到在触发通知时。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

 

 




