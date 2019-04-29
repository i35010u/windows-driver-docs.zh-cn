---
title: Windows 内核模式 HAL 库
description: Windows 内核模式 HAL 库
ms.assetid: 5cfdbf1b-b856-4a0c-9f56-3879482819aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7713713e19ee43bb0f47a149c08456ad850f22f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379347"
---
# <a name="windows-kernel-mode-hal-library"></a>Windows 内核模式 HAL 库


Windows 在多个不同配置的个人计算机上运行。 每个配置需要硬件和操作系统的其余部分之间进行交互的软件的层。 此层提取 （隐藏） 低级硬件驱动程序和操作系统的详细信息，因为它被称为硬件抽象层 (HAL)。

开发人员不建议编写其自己的 HAL。 如果需要硬件访问，HAL 库提供了可用于此目的的例程。 例程的 HAL 直接都带有前缀字母接口"**Hal**"; 有关 HAL 例程的列表，请参阅[硬件抽象层 (HAL) 库例程](https://msdn.microsoft.com/library/windows/hardware/ff546644)。

 

 




