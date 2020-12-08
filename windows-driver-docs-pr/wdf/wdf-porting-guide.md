---
title: 将驱动程序从 WDM 移植到 WDF
description: 本节中的主题介绍如何将现有的 WDM 驱动程序转换为 Kernel-Mode Driver Framework (KMDF) 驱动程序或 User-Mode Driver Framework (UMDF) 版本2驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2b7b9e0dd33f9dd484eedce31caf9627a0a0ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809785"
---
# <a name="porting-a-driver-from-wdm-to-wdf"></a>将驱动程序从 WDM 移植到 WDF


本节中的主题介绍如何将现有的 WDM 驱动程序转换为 Kernel-Mode Driver Framework (KMDF) 驱动程序或 User-Mode Driver Framework (UMDF) 版本2驱动程序。

从结构上讲，Windows 驱动程序框架 (WDF) 驱动程序与 WDM 驱动程序类似。 WDM 驱动程序由 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数、操作系统调用服务 i/o 请求的各种调度例程以及其他特定于驱动程序的实用工具函数组成。 WDF 驱动程序包括 [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 函数、框架调用服务 i/o 请求的各种事件回调函数以及其他特定于驱动程序的实用工具函数。 但是，在这种广泛的结构中，这两个模型具有重要的差异。

## <a name="in-this-section"></a>在本节中


-   [可以移植的具体驱动程序以及移植位置](which-drivers-can-be-ported.md)
-   [适用于 WDF 驱动程序的 WDM 概念](wdm-concepts-for-kmdf-drivers.md)
-   [WDM 和 WDF 之间的差异](differences-between-wdm-and-kmdf.md)
-   [准备移植](general-guidelines-for-porting.md)
-   [移植步骤](how-to-port.md)
-   [KMDF 和 WDM 等效项的摘要](summary-of-kmdf-and-wdm-equivalents.md)

 

