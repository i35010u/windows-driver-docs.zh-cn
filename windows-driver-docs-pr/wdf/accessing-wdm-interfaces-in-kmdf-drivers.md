---
title: KMDF 驱动程序中访问 WDM 接口
description: 大多数内核模式驱动程序框架 (KMDF) 驱动程序不需要直接访问 Windows 驱动程序模型 (WDM) 接口。
ms.assetid: 86e35617-cb6a-4d65-b2a6-9c7bcfa73480
keywords:
- 内核模式驱动程序 WDK KMDF WDM
- KMDF WDK WDM
- 内核模式驱动程序框架 WDK WDM
- 基于框架的驱动程序 WDK KMDF WDM
- WDM 接口 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34642883ad5f0d5e4045fca6ed4b3745bfdcc419
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545742"
---
# <a name="accessing-wdm-interfaces-in-kmdf-drivers"></a>KMDF 驱动程序中访问 WDM 接口


\[仅适用于 KMDF\]

大多数内核模式驱动程序框架 (KMDF) 驱动程序不需要直接访问 Windows 驱动程序模型 (WDM) 接口。 本部分介绍有限的情况下，当 KMDF 驱动程序需要直接访问 WDM 数据结构，例如若要获取 WDM 信息或处理 IRP。

## <a name="in-this-section"></a>本部分内容


-   [获取 WDM 信息](obtaining-wdm-information.md)
-   [处理框架外部的 WDM Irp](handling-wdm-irps-outside-of-the-framework.md)
-   [WDM 接口限制](wdm-interface-restrictions.md)

 

 





