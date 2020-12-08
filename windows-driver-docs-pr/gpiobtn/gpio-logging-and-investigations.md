---
title: GPIO 日志记录和调查
description: 本主题介绍 GPIO 测试的日志记录和调查。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d1eec90a2f45d6d31d64640abf29166644e3ce5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818459"
---
# <a name="gpio-logging-and-investigations"></a>GPIO 日志记录和调查


本主题介绍 GPIO 测试的日志记录和调查。

LogMan

``` syntax
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>

logman stop -ets buttonTrace
```

**注意**  
这是一个 WPP 跟踪。

 

如果测试失败，日志记录有助于诊断是否执行了适当的注入。 例如，如果需要更改插接指示器，则应在触发通知时在日志中找到以下条目。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

有关如何实现指示器注入的其他指导，请参阅 Windows 8.1 的 [GPIO 按钮和指示器实现指南](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)。

 

 




