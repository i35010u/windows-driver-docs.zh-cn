---
title: 处理 SRB_FUNCTION_RESET_DEVICE
description: 处理 SRB_FUNCTION_RESET_DEVICE
ms.assetid: d95bca21-306e-4598-a8c6-04990885e23d
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 156f4635de920238e7305c7ef25b854c369c91c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562564"
---
# <a name="handling-srbfunctionresetdevice"></a>处理 SRB\_函数\_重置\_设备


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


Scsi 端口驱动程序不能再将此 SRB 发送到其微型端口驱动程序。 仅 Storport 微型端口驱动程序可能必须处理此 SRB。

如果 HBA 能够重置的目标设备，指示何时[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)设置[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)，端口驱动程序将请求重置的未完成的请求超时时的设备。

系统端口驱动程序调用微型端口驱动程序*HwScsiStartIo*例程使用在其中 SRB**函数**成员设置为 SRB\_函数\_重置\_设备。 微型端口驱动程序负责完成收到重置设备请求时在设备上未完成的任何请求。

如果设备重置失败或超时，或等待端口驱动程序时，发生超时的时候**NextRequest**通知、 端口驱动程序调用[ *HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318).

 

 




