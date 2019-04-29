---
title: 从驱动程序树中删除项
description: 从驱动程序树中删除项
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 748b20929d4584d60359508128bc021a04b29526
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373217"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>从驱动程序树中删除项





若要删除的驱动程序项，WIA 服务调用微型驱动程序入口点[ **IWiaMiniDrv::drvDeleteItem**](https://msdn.microsoft.com/library/windows/hardware/ff543961)。 在此方法，微型驱动程序将尝试删除 WIA 服务上下文参数的项*pWiasContext*点。 如果成功删除该项，则该方法返回 S\_确定，并设置设备错误值参数， *plDevErrVal*、 为零。 如果设备出错，则方法返回失败和中的特定于设备的错误值*plDevErrVal*。 微型驱动程序应调用[ **wiasQueueEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549296)函数来通知所有连接的应用程序已删除了某项。

WIA 服务根项已被删除后，调用[ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543972)来释放使用的驱动程序特定的上下文的资源。 WIA 服务然后会删除项和特定于驱动程序的上下文。

 

 




