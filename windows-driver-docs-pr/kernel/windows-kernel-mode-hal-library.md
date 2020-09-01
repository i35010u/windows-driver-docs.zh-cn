---
title: Windows 内核模式 HAL 库
description: Windows 内核模式 HAL 库
ms.assetid: 5cfdbf1b-b856-4a0c-9f56-3879482819aa
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4258048ab9027472d4428d1f05196aed0c76c173
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184223"
---
# <a name="windows-kernel-mode-hal-library"></a>Windows 内核模式 HAL 库


Windows 在个人计算机的许多不同配置上运行。 每个配置都需要一个在硬件和其余操作系统之间进行交互的软件层。 由于此层抽象 (隐藏了驱动程序和操作系统) 低级别硬件详细信息，因此它被称为硬件抽象层 (HAL) 。

不鼓励开发人员编写自己的 HAL。 如果需要对硬件进行访问，HAL 库将提供可用于此目的的例程。 与 HAL 直接交互的例程以字母 "**HAL**" 作为前缀;有关 HAL 例程的列表，请参阅 [硬件抽象层 (HAL) 库例程](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。

 

