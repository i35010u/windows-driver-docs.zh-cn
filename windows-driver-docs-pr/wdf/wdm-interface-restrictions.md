---
title: WDM 接口限制
description: WDM 接口限制
keywords:
- KMDF WDK，WDM
- Kernel-Mode Driver Framework WDK，WDM
- WDM 驱动程序 WDK KMDF
- 基于框架的驱动程序 WDK KMDF，WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 431d4afce2c65304019f16f59ed3a97627ea4e5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840221"
---
# <a name="wdm-interface-restrictions"></a>WDM 接口限制


\[仅适用于 KMDF\]




如果你的基于框架的驱动程序访问 WDM 接口，你必须了解以下限制：

-   基于框架的驱动程序不得使用 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构的 **DriverContext** 成员，因为框架使用此成员。

 

