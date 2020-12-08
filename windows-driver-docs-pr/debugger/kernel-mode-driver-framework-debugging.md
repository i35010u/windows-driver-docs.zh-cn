---
title: 内核模式驱动程序框架调试
description: 内核模式驱动程序框架调试
keywords:
- Kernel-Mode Driver Framework 调试
- Windows Driver Foundation
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cb3dd98a686dc67aac63af6105e065876f45749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801915"
---
# <a name="kernel-mode-driver-framework-debugging"></a>内核模式驱动程序框架调试


Kernel-Mode Driver Framework (KMDF) 的调试扩展包含在 Wdfkd.dll 扩展库中。

你可以使用 Wdfkd.dll 扩展库包含的扩展命令来调试使用 KMDF 的驱动程序。

有关 Wdfkd.dll 中的扩展命令的说明，请参阅 [ ( # A1) 的内核模式驱动程序框架扩展 ](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)。

这些扩展可在 Microsoft Windows XP 和更高版本的操作系统上使用。 某些扩展具有其他限制;这些限制在各个参考页上注明。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果你的驱动程序名称超出最大长度，则你的驱动程序将无法加载。

 

若要使用此扩展库，必须将库加载到调试器中。 有关如何将扩展库加载到调试器中的信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

 

 





