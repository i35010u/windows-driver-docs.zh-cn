---
title: 锁定和解锁最佳做法
description: 锁定和解锁最佳做法
ms.assetid: cfa45c0d-4e92-4455-a8f6-17d4806f9c36
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 167e3219a286174f1e2f52659d0a6c75cdfe3847
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378853"
---
# <a name="locking-and-unlocking-best-practices"></a>锁定和解锁最佳做法





锁定 WIA 驱动程序的 STI 部分需要特别注意。 即使应用程序可以直接访问已发布的 STI 接口，此类直接访问设备可能会被误用。 锁定未正确实现的技术可能会使设备打开到拒绝服务 (DoS) 攻击。

### <a name="for-sti-applications"></a>对于 STI 应用程序

以下列表包含的预防措施和使用 STI 应用程序时应遵循以下的准则：

-   并不持有的锁的时间更长。

-   如果不需要直接访问设备，它可能可以通过使用 WIA 接口方法获取相同的信息。 这是更可取，因为 WIA 然后服务锁定为您的控件。

-   TWAIN 驱动程序的使用 STI [ **IStiUSD::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)方法来控制设备的访问权限。 当 TWAIN 驱动程序使用 STI 时，TWAIN 驱动程序负责控制锁定时间。

-   您可以创建它，以便仅实现**IStiUSD**接口方法。 这种方法的缺点是应用程序可以调用**IStiUSD::LockDevice**直接，从而锁定供独占使用的设备应用程序。 Windows 硬件质量实验室不认证使用这种方法; 的驱动程序此类驱动程序可以安装仅为未签名驱动程序。

### <a name="for-wia-drivers"></a>WIA 驱动程序

以下列表包含的预防措施和使用 WIA 驱动程序时应遵循的指导原则：

-   在长锁期间监视的设备的活动。 如果没有任何活动，该驱动程序应解锁设备，并允许其他客户端连接。 该驱动程序不应解锁设备，例如，如果它正在扫描非常大的图像，或者花费很长时间来获取的映像。 这会中断当前会话。 具体取决于设备和它对进行操作的总线，非常大的图像可以是任意位置从 10 兆字节到多个千兆字节，而长时间可以是任意位置从 500 毫秒超过一分钟的时间。 应基准测试你的设备和总线因此可以知道这些特定的值是为你的设备运行。

-   使用 WIA 的应用程序不会访问驱动程序的锁定方法[ **IWiaMiniDrv::drvLockWiaDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)并[ **IWiaMiniDrv::drvUnLockWiaDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice). WIA 服务仅 WIA 服务调用这些锁定方法时，会锁定调用传播**IStiUSD**使用**IStiUSD::LockDevice**方法。

-   如果应用程序以独占方式锁定 WIA 设备使用**IStiUSD::LockDevice**方法，该应用程序调用之前，WIA 服务无法访问设备[ **IStiUSD::UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice)方法。 如果 WIA 服务不能锁定该设备，设备将不能对任何应用程序或驱动程序依赖于 WIA 服务。

-   [ **IWiaMiniDrv::drvLockWiaDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)方法应始终调用[ **IStiDevice::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice)方法，并[ **IWiaMiniDrv::drvUnLockWiaDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)方法应始终调用[ **IStiDevice::UnLockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice)方法。 这可确保 WIA 服务执行适当锁定管理设备。 **IStiDevice**接口传递给对的调用中的驱动程序[ **IWiaMiniDrv::drvInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)方法。 此接口应缓存，用于调用**IStiDevice::LockDevice**方法。 此方法将调用您的驱动程序**IStiUSD::LockDevice**方法。

-   如果布尔值用于控制锁定，防止多个线程此值。 当两个驱动程序尝试在同一时间锁定单个设备时，才能成功只有一个驱动程序。

 

 




