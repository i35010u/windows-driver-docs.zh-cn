---
title: 将驱动程序从 WDM 移植到 WDF
description: 在本部分中的主题介绍如何将现有 WDM 驱动程序转换为内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序。
ms.assetid: 3B4D677D-2FCC-45A1-95B4-DA9CA9D7B452
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f637734d3bd5a8902166bd6e36b0cc237d18eaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372099"
---
# <a name="porting-a-driver-from-wdm-to-wdf"></a>将驱动程序从 WDM 移植到 WDF


在本部分中的主题介绍如何将现有 WDM 驱动程序转换为内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序。

体系结构方面，Windows 驱动程序框架 (WDF) 驱动程序是类似于 WDM 驱动程序。 WDM 驱动程序组成[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数，各种调度操作系统到 I/O 请求提供服务和其他特定于驱动程序的实用工具函数将调用的例程。 WDF 驱动程序组成[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)函数、 各种事件回叫函数，为 I/O 请求提供服务，框架将调用和其他特定于驱动程序的实用工具函数。 但是，在此广泛结构中，两个模型有重要差异。

## <a name="in-this-section"></a>本节内容


-   [该驱动程序可以移植和位置](which-drivers-can-be-ported.md)
-   [WDF 驱动程序的 WDM 概念](wdm-concepts-for-kmdf-drivers.md)
-   [WDM 和 WDF 之间的差异](differences-between-wdm-and-kmdf.md)
-   [为迁移准备](general-guidelines-for-porting.md)
-   [在移植的步骤](how-to-port.md)
-   [KMDF 和 WDM 等效项的摘要](summary-of-kmdf-and-wdm-equivalents.md)

 

 





