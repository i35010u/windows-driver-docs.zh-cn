---
title: 取消数据传输
description: 取消数据传输
ms.assetid: a7900968-df57-41d9-abb1-4d2c97517362
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2565f99a249e30c3587a90080b1f99a654ac04dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366731"
---
# <a name="canceling-a-data-transfer"></a>取消数据传输





WIA 应用程序和 WIA 微型驱动程序可以在任何时候取消数据传输。 WIA 微型驱动程序可以确定应用程序是否通过检查返回的值取消数据传输[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)方法。 如果该方法返回 S\_为 FALSE，数据传输已取消。 WIA 微型驱动程序必须停止获取的所有活动，并返回到空闲状态。 然后，它就可以进行下一步的数据传输。

WIA 微型驱动程序可以发出信号返回已取消数据传输 S\_从 FALSE [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法。 某些设备具有可以中止数据传输的硬件上的取消按钮。 在这种情况下，WIA 微型驱动程序应返回 S\_FALSE。

**请注意**  就可以取消 WIA 扫描而无需声明错误并返回 S\_FALSE。 但是，这是仅可以在 Windows XP 和更高版本的操作系统;不能在 Windows Millennium Edition。

 

所有返回代码从收到**IWiaMiniDrvCallBack::MiniDrvCallback**方法应返回在**IWiaMiniDrv::drvAcquireItemData**方法。 如果应用程序返回错误代码**IWiaMiniDrvCallBack::MiniDrvCallback**方法，WIA 微型驱动程序必须停止数据传输，返回到错误代码为 WIA 服务空闲状态，然后返回。

 

 




