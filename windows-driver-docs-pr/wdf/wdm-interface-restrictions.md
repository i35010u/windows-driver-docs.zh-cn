---
title: WDM 接口限制
description: WDM 接口限制
ms.assetid: 89f3793e-8561-4d8a-a01a-1ff7aecca64a
keywords:
- KMDF WDK WDM
- 内核模式驱动程序框架 WDK WDM
- WDM 驱动程序 WDK KMDF
- 基于框架的驱动程序 WDK KMDF WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9261cc1a0d48b4b79a0782bb623fe6cff2f50fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372081"
---
# <a name="wdm-interface-restrictions"></a>WDM 接口限制


\[仅适用于 KMDF\]




如果您基于 framework 的驱动程序访问 WDM 接口，则必须注意以下限制：

-   基于框架的驱动程序必须使用**Tail.Overlay.DriverContext**的成员[ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)结构，因为框架将使用此成员。

 

 





