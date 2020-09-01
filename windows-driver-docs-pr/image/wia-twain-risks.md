---
title: WIA-TWAIN 风险
description: WIA-TWAIN 风险
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774d388ee053b773282a336ee6cac4bf0aebdc59
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191189"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN 风险





如果你的 TWAIN 驱动程序使用 WIA 驱动程序的 STI 部分，则需要注意以下事项：

1.  在访问驱动程序之前，TWAIN 数据源会调用 [**IStiUSD：： LockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice) 。 这会阻止 WIA 应用程序连接到 WIA 驱动程序，直到调用 [**IStiUSD：： UnLockDevice**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice) 。 若要最大程度地减少此问题，请保持对设备的访问权限，使 WIA 客户端可以连接和执行操作。 这一点很重要，因为 TWAIN 维护应用程序和驱动程序之间的一对一关系。 WIA 允许将多个应用程序连接到单个 WIA 驱动程序。 出于此原因，访问 TWAIN 驱动程序的 TWAIN 应用程序可能会锁定 WIA 应用程序。 若要防止出现这种情况，请使用正确的锁定方法。

2.  任何使用 STI 接口方法的应用程序或实用工具都可以阻止对 WIA 驱动程序的访问。 一些示例包括监视按钮或设备状态的实用程序以及监视系统任务栏的应用程序。

3.  WIA 驱动程序应确保对 [**IStiUSD：： RawReadData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)、 [**IStiUSD：： RawWriteData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)、 [**IStiUSD：： RawReadCommand**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand)、 [**IStiUSD：： RawWriteCommand**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand) 和 [**IStiUSD：： Escape**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape) 的调用使用正确的锁定进行了适当的验证和隔离。

当你编写驱动程序时，请验证传入值，以便仅将有效数据发送到设备。

若要在使用 **IStiUSD：： escape**时正确验证顺序，请参阅 [使用 IStiUSD 转义方法](using-the-istiusd-escape-method.md)。 有关正确锁定的其他信息，请参阅 [锁定和解锁最佳实践](locking-and-unlocking-best-practices.md)。

 

