---
title: 用户模式驱动程序框架扩展 (Wudfext.dll)
description: 用户模式驱动程序框架扩展 (Wudfext.dll)
keywords:
- '用户模式驱动程序框架扩展 ( # A0) '
- '用户模式驱动程序框架调试，扩展 ( # A0) '
- 'wudfext.dll (用户模式驱动程序框架扩展) '
- 扩展，用户模式驱动程序框架
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5b0b28861ada5e6877cdc0e4773e41f5c6fc17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803235"
---
# <a name="user-mode-driver-framework-extensions-wudfextdll"></a>用户模式驱动程序框架扩展 (Wudfext.dll)


Wudfext.dll 中实现了用于调试 User-Mode Driver Framework 驱动程序的扩展命令。

某些扩展对所需的 Windows 版本或 UMDF 版本具有额外限制;这些限制在各个参考页上注明。

**注意**  在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。 如果你的驱动程序名称超出最大长度，则你的驱动程序将无法加载。

 

有关使用这些扩展的方法，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

 

 





