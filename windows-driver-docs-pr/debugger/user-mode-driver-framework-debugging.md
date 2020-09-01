---
title: 用户模式驱动程序框架调试
description: 用户模式驱动程序框架调试
ms.assetid: f59a420e-57d3-4ae0-84e3-58ec6e088b63
keywords:
- 用户模式驱动程序框架调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e25e4e5c15c2de6c8e655137cdbff4fb672d7ba
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215690"
---
# <a name="user-mode-driver-framework-debugging"></a>用户模式驱动程序框架调试

有关如何调试用户模式驱动程序框架 (UMDF) 驱动程序的概述，包括有关如何启动此类调试会话的信息，请参阅 [如何启用 UMDF 驱动程序调试](../wdf/enabling-a-debugger.md)。

### <a name="umdf-debugging-extensions"></a>UMDF 调试扩展

在扩展模块 Wudfext.dll 中实现了用户模式驱动程序框架 (UMDF) 调试扩展。 你可以使用这些扩展来调试使用 UMDF 的驱动程序。

有关 Wudfext.dll 中扩展命令的完整说明，请参阅 [# A1)  ( 用户模式驱动程序框架扩展 ](user-mode-driver-framework-extensions--wudfext-dll-.md)。

某些扩展对所需的 Windows 版本或 UMDF 版本具有额外限制;这些限制在各个参考页上注明。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果你的驱动程序名称超出最大长度，则你的驱动程序将无法加载。

若要使用此扩展库，必须将库加载到调试器中。 有关如何将扩展库加载到调试器中的信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。