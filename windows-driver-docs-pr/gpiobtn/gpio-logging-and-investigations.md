---
title: GPIO 日志记录和调查
description: 本主题介绍日志记录和调查的 GPIO 测试。
ms.assetid: 998BF6BC-D931-4555-A8BC-F860DFA9A18F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b01e4045b0c8e7f2a2acaf32bbf6ad289968430a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544390"
---
# <a name="gpio-logging-and-investigations"></a>GPIO 日志记录和调查


本主题介绍日志记录和调查的 GPIO 测试。

LogMan:

``` syntax
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>

logman stop -ets buttonTrace
```

**请注意**  这是 WPP 跟踪。

 

如果测试失败，日志记录可以帮助诊断是否执行了相应的注入。 例如，如果希望停靠指示器更改，以下条目应是日志中找到在触发通知时。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

有关如何实现指示器注入的其他指南，请参阅[Windows 8.1 的 GPIO 按钮和指示器实施指南](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)。

 

 




