---
title: Windows 内核模式运行时库
description: Windows 内核模式运行时库
ms.assetid: 9c968014-c529-43e1-a8a6-a307c90e4162
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 139c31f28a86cae28bfe894f3a04b3a520cfa0cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838308"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows 内核模式运行时库


Windows 提供了各种内核模式组件所需的一组常用实用程序例程。 例如， [**RtlCheckRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)用于查看某个给定的密钥是否在注册表中。

大多数运行时库（RTL）例程都带有字母 "**RTL**" 的前缀;有关内核的运行时库例程列表，请参阅[运行时库（RTL）例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

还有一个专门为安全字符串处理设计的不同内核模式库。 有关安全字符串库的详细信息，请参阅[Windows 内核模式安全字符串库](windows-kernel-mode-safe-string-library.md)。 请注意，安全字符串库例程通常采用 "**Rtl**" 前缀，但不是运行时库（Rtl）的一部分。

 

 




