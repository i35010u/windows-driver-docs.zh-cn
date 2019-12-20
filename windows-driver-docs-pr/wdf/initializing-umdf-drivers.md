---
title: 初始化 UMDF 驱动程序
description: 初始化 UMDF 驱动程序
ms.assetid: b21ec019-1a80-4219-8aa8-3545ec3383b9
keywords:
- 用户模式驱动程序框架 WDK，初始化驱动程序
- UMDF WDK，初始化驱动程序
- 用户模式驱动程序 WDK UMDF，初始化
- 初始化驱动程序 WDK UMDF
- 发送程序 WDK UMDF
- 加载发送程序 WDK UMDF
- 驱动程序主机进程 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cc52ae8cbb8632056be8ab806be1742f9451a28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210043"
---
# <a name="initializing-umdf-drivers"></a>初始化 UMDF 驱动程序


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

在初始化设备的 UMDF 驱动程序之前，会通过操作系统加载驱动程序管理器和反射器，并创建驱动程序主机进程。 若要确保设备成功启动，则会在反射器初始化时加载并完全初始化驱动程序管理器。

安装设备后，如果尚未加载，即插即用（PnP）子系统将加载反射器。 然后，反射器联系驱动程序管理器以创建驱动程序主机进程。 然后，新创建的驱动程序主机进程中的框架将调用[**IDriverEntry：： OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法来初始化 UMDF 驱动程序（如果尚未初始化）。

框架为驱动程序主机进程中加载的每个设备添加新的设备对象。 以下部分显示了概述，并详细介绍了框架如何添加新设备：

-   [添加设备概述](adding-a-device-overview.md)
-   [添加设备](adding-a-device.md)

 

 





