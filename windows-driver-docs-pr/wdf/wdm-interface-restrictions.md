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
ms.openlocfilehash: 39bbe87a759ce088a9c95b690f5ee64fce3b804d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385712"
---
# <a name="wdm-interface-restrictions"></a>WDM 接口限制


\[仅适用于 KMDF\]




如果您基于 framework 的驱动程序访问 WDM 接口，则必须注意以下限制：

-   基于框架的驱动程序必须使用**Tail.Overlay.DriverContext**的成员[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)结构，因为框架将使用此成员。

 

 





