---
title: WIA-TWAIN 风险
description: WIA-TWAIN 风险
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d300da635a5e7267c66c7694fe3865df808f937a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840665"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN 风险





如果你的 TWAIN 驱动程序使用 WIA 驱动程序的 STI 部分，则需要注意以下事项：

1.  在访问驱动程序之前，TWAIN 数据源会调用[**IStiUSD：： LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice) 。 这会阻止 WIA 应用程序连接到 WIA 驱动程序，直到调用[**IStiUSD：： UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice) 。 若要最大程度地减少此问题，请保持对设备的访问权限，使 WIA 客户端可以连接和执行操作。 这一点很重要，因为 TWAIN 维护应用程序和驱动程序之间的一对一关系。 WIA 允许将多个应用程序连接到单个 WIA 驱动程序。 出于此原因，访问 TWAIN 驱动程序的 TWAIN 应用程序可能会锁定 WIA 应用程序。 若要防止出现这种情况，请使用正确的锁定方法。

2.  任何使用 STI 接口方法的应用程序或实用工具都可以阻止对 WIA 驱动程序的访问。 一些示例包括监视按钮或设备状态的实用程序以及监视系统任务栏的应用程序。

3.  WIA 驱动程序应确保对[**IStiUSD：： RawReadData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)、 [**IStiUSD：： RawWriteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)、 [**IStiUSD：： RawReadCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand)、 [**IStiUSD：： RawWriteCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)和[**IStiUSD：： Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)的调用经过适当的验证和隔离使用正确的锁定。

当你编写驱动程序时，请验证传入值，以便仅将有效数据发送到设备。

若要在使用**IStiUSD：： escape**时正确验证顺序，请参阅[使用 IStiUSD 转义方法](using-the-istiusd-escape-method.md)。 有关正确锁定的其他信息，请参阅[锁定和解锁最佳实践](locking-and-unlocking-best-practices.md)。

 

 




