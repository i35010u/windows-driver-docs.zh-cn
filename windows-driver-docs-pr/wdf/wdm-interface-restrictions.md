---
title: WDM 接口限制
description: WDM 接口限制
ms.assetid: 89f3793e-8561-4d8a-a01a-1ff7aecca64a
keywords:
- KMDF WDK，WDM
- 内核模式驱动程序框架 WDK，WDM
- WDM 驱动程序 WDK KMDF
- 基于框架的驱动程序 WDK KMDF，WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d51262c98885d99bf918c9beabb7338b9fb34af6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186235"
---
# <a name="wdm-interface-restrictions"></a>WDM 接口限制


\[仅适用于 KMDF\]




如果你的基于框架的驱动程序访问 WDM 接口，你必须了解以下限制：

-   基于框架的驱动程序不得使用[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构的**DriverContext**成员，因为框架使用此成员。

 

