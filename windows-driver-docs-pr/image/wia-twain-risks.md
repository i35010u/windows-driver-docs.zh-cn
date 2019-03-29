---
title: WIA-TWAIN 风险
description: WIA-TWAIN 风险
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a909adfab1ad4e80d2498777bec2785ef3cb6aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577053"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN 风险





如果必须使用 WIA 驱动程序的 STI 部分 TWAIN 驱动程序，需要注意以下内容：

1.  TWAIN 数据源调用[ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)才能访问该驱动程序。 这可以防止 WIA 应用程序连接到您 WIA 的驱动程序直到[ **IStiUSD::UnLockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543843)调用。 为了尽量减少此问题，保留到设备限制使 WIA 客户端可以连接并执行操作的访问权限。 这一点很重要因为 TWAIN 维护应用程序和驱动程序之间的一对一关系。 WIA 允许多个应用程序连接到单个 WIA 驱动程序。 出于此原因，访问 TWAIN 驱动程序的 TWAIN 应用程序可能可以锁定 WIA 应用程序。 若要防止此情况，使用适当的锁定方法。

2.  任何应用程序或使用 STI 接口方法的实用程序可防止对 WIA 驱动程序访问。 一些示例是监视按钮或设备状态和监视系统任务栏的应用程序的实用工具。

3.  WIA 驱动程序应确保为调用[ **IStiUSD::RawReadData**](https://msdn.microsoft.com/library/windows/hardware/ff543834)， [ **IStiUSD::RawWriteData**](https://msdn.microsoft.com/library/windows/hardware/ff543839)， [ **IStiUSD::RawReadCommand**](https://msdn.microsoft.com/library/windows/hardware/ff543831)， [ **IStiUSD::RawWriteCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543836)并[ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)正确验证和使用适当的锁定来隔离。

编写您的驱动程序，验证传入因此唯一有效的值时数据发送到设备。

使用时的适当的验证序列**IStiUSD::Escape**，请参阅[使用 IStiUSD 转义方法](using-the-istiusd-escape-method.md)。 有关正确地锁定的其他信息，请参阅[锁定和解锁的最佳实践](locking-and-unlocking-best-practices.md)。

 

 




