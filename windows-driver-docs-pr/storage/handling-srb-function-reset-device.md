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
ms.openlocfilehash: 28611b80631ab5b2bc0319b6f8bbd1a0278603fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372334"
---
# <a name="handling-srbfunctionresetdevice"></a>处理 SRB\_函数\_重置\_设备


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


Scsi 端口驱动程序不能再将此 SRB 发送到其微型端口驱动程序。 仅 Storport 微型端口驱动程序可能必须处理此 SRB。

如果 HBA 能够重置的目标设备，指示何时[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))设置[**端口\_配置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)，端口驱动程序将请求重置的未完成的请求超时时的设备。

系统端口驱动程序调用微型端口驱动程序*HwScsiStartIo*例程使用在其中 SRB**函数**成员设置为 SRB\_函数\_重置\_设备。 微型端口驱动程序负责完成收到重置设备请求时在设备上未完成的任何请求。

如果设备重置失败或超时，或等待端口驱动程序时，发生超时的时候**NextRequest**通知、 端口驱动程序调用[ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)).

 

 




