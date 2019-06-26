---
title: Windows 内核模式 HAL 库
description: Windows 内核模式 HAL 库
ms.assetid: 5cfdbf1b-b856-4a0c-9f56-3879482819aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a9d1e723dfef0cb4e6e8709244e8f8cc4aad1c0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358058"
---
# <a name="windows-kernel-mode-hal-library"></a>Windows 内核模式 HAL 库


Windows 在多个不同配置的个人计算机上运行。 每个配置需要硬件和操作系统的其余部分之间进行交互的软件的层。 此层提取 （隐藏） 低级硬件驱动程序和操作系统的详细信息，因为它被称为硬件抽象层 (HAL)。

开发人员不建议编写其自己的 HAL。 如果需要硬件访问，HAL 库提供了可用于此目的的例程。 例程的 HAL 直接都带有前缀字母接口"**Hal**"; 有关 HAL 例程的列表，请参阅[硬件抽象层 (HAL) 库例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。

 

 




