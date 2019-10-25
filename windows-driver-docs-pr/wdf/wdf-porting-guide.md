---
title: 将驱动程序从 WDM 移植到 WDF
description: 本节中的主题介绍如何将现有 WDM 驱动程序转换为内核模式驱动程序框架（KMDF）驱动程序或用户模式驱动程序框架（UMDF）版本2驱动程序。
ms.assetid: 3B4D677D-2FCC-45A1-95B4-DA9CA9D7B452
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a07228b1f5d56061f319fd7736f11577c40e72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845416"
---
# <a name="porting-a-driver-from-wdm-to-wdf"></a>将驱动程序从 WDM 移植到 WDF


本节中的主题介绍如何将现有 WDM 驱动程序转换为内核模式驱动程序框架（KMDF）驱动程序或用户模式驱动程序框架（UMDF）版本2驱动程序。

从结构上讲，Windows 驱动程序框架（WDF）驱动程序与 WDM 驱动程序类似。 WDM 驱动程序由[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数、操作系统调用服务 i/o 请求的各种调度例程以及其他特定于驱动程序的实用工具函数组成。 WDF 驱动程序包括[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)函数、框架调用服务 i/o 请求的各种事件回调函数以及其他特定于驱动程序的实用工具函数。 但是，在这种广泛的结构中，这两个模型具有重要的差异。

## <a name="in-this-section"></a>本部分内容


-   [可移植的驱动程序和](which-drivers-can-be-ported.md)
-   [WDF 驱动程序的 WDM 概念](wdm-concepts-for-kmdf-drivers.md)
-   [WDM 与 WDF 之间的差异](differences-between-wdm-and-kmdf.md)
-   [准备迁移](general-guidelines-for-porting.md)
-   [移植步骤](how-to-port.md)
-   [KMDF 和 WDM 等效项摘要](summary-of-kmdf-and-wdm-equivalents.md)

 

 





