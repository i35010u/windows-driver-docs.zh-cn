---
title: DDI 合规性规则
description: DDI 合规性规则
ms.assetid: f020fff9-f880-4aa8-b422-5452728d2fdd
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d1261b3e37bef67b11d9b3844abed2b3c2e1cdef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345755"
---
# <a name="ddi-compliance-rules"></a>DDI 合规性规则


本部分列出并描述可用于验证 Windows 驱动程序模型 (WDM)、 内核模式驱动程序框架 (KMDF)、 音频 (PortCls)、 AVStream (KS)、 NDIS 和 Storport 驱动程序的 Windows 设备驱动程序接口 (DDI) 符合性规则。 DDI 符合性规则定义一个驱动程序和操作系统的内核接口之间的正确交互的要求。

[音频驱动程序的规则](rules-for-audio-drivers.md)  
[有关 AVStream 驱动程序的规则](rules-for-avstream-drivers.md)  
[用于 WDM 驱动程序的规则](sdv-rules-for-wdm-drivers.md)  
[用于 KMDF 驱动程序的规则](sdv-rules-for-kmdf-drivers.md)  
[NDIS 驱动程序的规则](sdv-rules-for-ndis-drivers.md)  
[Storport 驱动程序的规则](sdv-rules-for-storport-drivers.md)  

### <a name="driver-verification-tools"></a>驱动程序验证工具

可以使用代码分析工具， [Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)并[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)若要测试到 DDI 使用规则的符合性的驱动程序。 因此，可以在开发周期的早期使用 SDV，static Driver Verifier (SDV) 对驱动程序源代码中，执行静态分析。 驱动程序验证程序与操作系统，集成，因此您可以测试在运行时的驱动程序之后它已生成、 部署，并已安装。

使用驱动程序的源代码， [Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)创建模型的驱动程序和操作系统。 在此模型中，SDV 将放在恶意环境中的驱动程序和系统地测试代码路径通过驱动程序通过查找正式化组驱动程序符合性规则的冲突 ([Static Driver Verifier 规则](https://msdn.microsoft.com/library/windows/hardware/ff552839))。

从 Windows 8 开始，你可以配置[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)若要运行的一些符合性检查安装的驱动程序，从而[DDI 符合性检查](https://msdn.microsoft.com/library/windows/hardware/hh454208)。

## <a name="related-topics"></a>相关主题


[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)
[的 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)
 

 





