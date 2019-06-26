---
title: Windows 内核模式运行时库
description: Windows 内核模式运行时库
ms.assetid: 9c968014-c529-43e1-a8a6-a307c90e4162
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1adf71f4f0eab0d05c9b809bb411f35ad2c65fbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374167"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows 内核模式运行时库


Windows 提供一的组不同的内核模式组件所需的常见实用工具例程。 例如， [ **RtlCheckRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcheckregistrykey)用于给定的密钥是否在注册表中。

运行时库 (RTL) 例程的大多数都带有前缀字母"**Rtl**"; 有关内核，运行时库例程的列表，请参阅[运行时库 (RTL) 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

此外，还有一个不同的内核模式库，专为安全字符串处理。 有关安全的字符串库的详细信息，请参阅[Windows 内核模式安全字符串库](windows-kernel-mode-safe-string-library.md)。 请注意通过安全的字符串库例程还通常作为前缀"**Rtl**"但不是运行时库 (RTL) 的一部分。

 

 




