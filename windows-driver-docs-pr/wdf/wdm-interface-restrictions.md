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
ms.openlocfilehash: aa7ed080c118df0c0fb4974384207a9c9eae944c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842795"
---
# <a name="wdm-interface-restrictions"></a>WDM 接口限制


\[仅适用于 KMDF\]




如果你的基于框架的驱动程序访问 WDM 接口，你必须了解以下限制：

-   基于框架的驱动程序不得使用[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构的**DriverContext**成员，因为框架使用此成员。

 

 





