---
title: 智能卡驱动程序调试
description: 智能卡驱动程序调试
ms.assetid: 701528f6-d8ba-4a73-ad68-cb35497a3474
keywords:
- 智能卡驱动程序 WDK，调试
- 调试驱动程序 WDK 智能卡
- DebugLevel
- 供应商提供的驱动程序 WDK 智能卡调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5703850f2a821293a24e90169b10509c48ca4ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392115"
---
# <a name="smart-card-driver-debugging"></a>智能卡驱动程序调试


## <span id="_ntovr_smart_card_driver_debugging"></span><span id="_NTOVR_SMART_CARD_DRIVER_DEBUGGING"></span>


智能卡驱动程序库支持几种调试功能。 每个调试功能都由中定义的以下常量之一*Smclib.h*标头文件：

```cpp
DEBUG_IOCTL
DEBUG_ATR
DEBUG_PROTOCOL
DEBUG_DRIVER
DEBUG_TRACE
DEBUG_ERROR
DEBUG_BREAK
DEBUG_ALL
```

由名为的值表示已启用调试功能的合集*调试级别*。 可以通过执行对应于你想要启用的功能的常量的按位或计算此值。

有两种方法来设置调试级别。 首先，您可以使用智能卡驱动程序测试程序， *Scdrvtst*，都使用 Windows Driver Kit (WDK)。 第二个是使用[ **SmartcardSetDebugLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff548960)智能卡驱动程序库例程。

在这两种情况下，必须将所需的调试级别的值传递给程序或例程，用于设置调试级别。 例如，若要使用智能卡库例程从驱动程序设置调试级别，进行以下调用：

```cpp
SmartcardSetDebugLevel(DebugLevel);
```

**重要**  必须安装操作系统的经检查的版本和驱动程序获取调试消息的经检查的版本。

 

若要编写从读取器驱动程序，该驱动程序调试消息必须调用以下例程：

```cpp
SmartcardDebug(
 ULONG DebugLevel,
 PCHAR Message
);
```

此例程还可用来按以下方式将消息写入到远程调试器。

-   若要编写错误消息，使用调试\_错误常量*DebugLevel*。

-   若要编写的标准驱动程序的消息，使用调试\_驱动程序常量。

-   若要编写跟踪消息，以表明读卡器驱动程序将进入或退出例程时，使用调试\_作为跟踪*DebugLevel*。

在开发驱动程序，使用智能卡驱动程序库的经检查的版本并将调试级别设置为最大值，通过使用**SmartcardSetDebugLevel**(调试\_所有) 在你*DriverEntry*例程。

有关设置远程调试会话的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。

 

 





