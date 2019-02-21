---
title: 取消数据传输
description: 取消数据传输
ms.assetid: a7900968-df57-41d9-abb1-4d2c97517362
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 855f4a1ccd9d1d094fd345e9c29873392bcea2f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542130"
---
# <a name="canceling-a-data-transfer"></a>取消数据传输





WIA 应用程序和 WIA 微型驱动程序可以在任何时候取消数据传输。 WIA 微型驱动程序可以确定应用程序是否通过检查返回的值取消数据传输[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)方法。 如果该方法返回 S\_为 FALSE，数据传输已取消。 WIA 微型驱动程序必须停止获取的所有活动，并返回到空闲状态。 然后，它就可以进行下一步的数据传输。

WIA 微型驱动程序可以发出信号返回已取消数据传输 S\_从 FALSE [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)方法。 某些设备具有可以中止数据传输的硬件上的取消按钮。 在这种情况下，WIA 微型驱动程序应返回 S\_FALSE。

**请注意**  就可以取消 WIA 扫描而无需声明错误并返回 S\_FALSE。 但是，这是仅可以在 Windows XP 和更高版本的操作系统;不能在 Windows Millennium Edition。

 

所有返回代码从收到**IWiaMiniDrvCallBack::MiniDrvCallback**方法应返回在**IWiaMiniDrv::drvAcquireItemData**方法。 如果应用程序返回错误代码**IWiaMiniDrvCallBack::MiniDrvCallback**方法，WIA 微型驱动程序必须停止数据传输，返回到错误代码为 WIA 服务空闲状态，然后返回。

 

 




