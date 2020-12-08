---
title: 锁定和解锁最佳做法
description: 锁定和解锁最佳做法
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: cce5ca0c2afd02550d42555500b8ddf19bc0e030
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824099"
---
# <a name="locking-and-unlocking-best-practices"></a>锁定和解锁最佳做法





为 WIA 驱动程序的 STI 部分进行锁定需要特别注意。 即使应用程序可以直接访问已发布的 STI 接口，也可以滥用对设备的直接访问。 不正确实现的锁定方法会使设备进入拒绝服务 (DoS) 攻击。

### <a name="for-sti-applications"></a>对于 STI 应用程序

下面的列表包含使用 STI 应用程序时应遵循的注意事项和指导原则：

-   不要长时间持有锁。

-   如果不需要直接访问设备，则可以使用 WIA 接口方法获取相同的信息。 这是首选方案，因为 WIA 服务随后会控制锁定。

-   使用 STI 的 TWAIN 驱动程序使用 [**IStiUSD：： LockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice) 方法来控制对设备的访问。 当 TWAIN 驱动程序使用 STI 时，TWAIN 驱动程序负责控制锁定时间。

-   您可以创建它，以便它仅实现 **IStiUSD** 接口方法。 此方法的缺点是，应用程序可以直接调用 **IStiUSD：： LockDevice** ，从而锁定设备以便应用程序独占使用。 Windows 硬件质量实验室不能使用此方法来验证驱动程序;此类驱动程序只能作为未签名的驱动程序安装。

### <a name="for-wia-drivers"></a>对于 WIA 驱动程序

下面的列表包含使用 WIA 驱动程序时应遵循的注意事项和指南：

-   在长时间锁定期间监视设备的活动。 如果没有任何活动，则驱动程序应解锁设备，并允许其他客户端连接。 驱动程序不应解锁设备，例如，如果扫描的是非常大的映像，或者需要很长时间才能获取映像。 这会中断当前会话。 非常大的映像可能会从 10 mb 到超过 1 gb，并且长时间可能介于500毫秒到超过一分钟的时间，具体取决于设备以及它所操作的总线。 应该对设备和它所操作的总线进行基准测试，以了解这些特定值对于设备是什么。

-   使用 WIA 的应用程序不访问驱动程序的锁定方法， [**IWiaMiniDrv：:D rvlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice) 和 [**IWiaMiniDrv：:d rvunlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)。 只有 WIA 服务调用这些锁定方法，WIA 服务使用 **IStiUSD：： LockDevice** 方法将锁定调用传播到 **IStiUSD** 。

-   如果应用程序使用 **IStiUSD：： LockDevice** 方法独占锁定 WIA 设备，则在该应用程序调用 [**IStiUSD：： UnLockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice) 方法之前，WIA 服务无法访问设备。 如果 WIA 服务无法锁定设备，则设备将不能用于依赖于 WIA 服务的任何应用程序或驱动程序。

-   [**IWiaMiniDrv：:D rvlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)方法应始终调用 [**IStiDevice：： LockDevice**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)方法， [**IWiaMiniDrv：:d Rvunlockwiadevice**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)方法应始终调用 [**IStiDevice：： UnLockDevice**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)方法。 这可确保 WIA 服务为设备执行适当的锁定管理。 在对 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法的调用中， **IStiDevice** 接口将传递给驱动程序。 应缓存此接口并使用它来调用 **IStiDevice：： LockDevice** 方法。 此方法调用驱动程序的 **IStiUSD：： LockDevice** 方法。

-   如果使用布尔值来控制锁定，请从多个线程中保护该值。 当两个驱动程序尝试同时锁定单个设备时，只有一个驱动程序可以成功。

 

