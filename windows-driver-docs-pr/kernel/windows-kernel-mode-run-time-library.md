---
title: Windows 内核模式运行时库
description: Windows 内核模式运行时库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d39ef832cef04f8247719aecb99a5d2bbf8b988c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836373"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows 内核模式运行时库


Windows 提供了各种内核模式组件所需的一组常用实用程序例程。 例如， [**RtlCheckRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey) 用于查看某个给定的密钥是否在注册表中。

大多数 (RTL) 例程的运行时库都带有字母 "**RTL**" 的前缀;有关内核的运行时库例程列表，请参阅 [ (RTL) 例程的运行时库](/windows-hardware/drivers/ddi/index)。

还有一个专门为安全字符串处理设计的不同内核模式库。 有关安全字符串库的详细信息，请参阅 [Windows Kernel-Mode 安全字符串库](windows-kernel-mode-safe-string-library.md)。 请注意，安全字符串库例程通常采用 "**Rtl**" 前缀，但并不是运行库 (Rtl) 的一部分。

 

