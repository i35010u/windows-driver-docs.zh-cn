---
title: 在 KMDF 驱动程序中访问 WDM 接口
description: 大多数 Kernel-Mode Driver Framework (KMDF) 驱动程序无需直接访问 Windows 驱动模型 (WDM) 接口。
keywords:
- 内核模式驱动程序 WDK KMDF，WDM
- KMDF WDK，WDM
- Kernel-Mode Driver Framework WDK，WDM
- 基于框架的驱动程序 WDK KMDF，WDM
- WDM 接口 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c67f3d2b69fc336e72507f4a295ba5c98dad6a3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811321"
---
# <a name="accessing-wdm-interfaces-in-kmdf-drivers"></a>在 KMDF 驱动程序中访问 WDM 接口


\[仅适用于 KMDF\]

大多数 Kernel-Mode Driver Framework (KMDF) 驱动程序无需直接访问 Windows 驱动模型 (WDM) 接口。 本部分介绍当 KMDF 驱动程序需要直接访问 WDM 数据结构（例如获取 WDM 信息或操作 IRP）时的有限情况。

## <a name="in-this-section"></a>在本节中


-   [获取 WDM 信息](obtaining-wdm-information.md)
-   [在框架外部处理 WDM IRP](handling-wdm-irps-outside-of-the-framework.md)
-   [WDM 接口限制](wdm-interface-restrictions.md)

 

 





