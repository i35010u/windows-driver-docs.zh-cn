---
title: 处理 SRB_FUNCTION_RESET_DEVICE
description: 处理 SRB_FUNCTION_RESET_DEVICE
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a62deeacdba755b9048a87110613e29cb9cc695
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804507"
---
# <a name="handling-srb_function_reset_device"></a>处理 SRB \_ 函数 \_ 重置 \_ 设备


## <span id="ddk_handling_srb_function_reset_device_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_DEVICE_KG"></span>


ScsiPort 驱动程序不再将此 SRB 发送到其微型端口驱动程序。 只有 Storport 微型端口驱动程序才能处理此 SRB。

如果 HBA 能够重置目标设备，如 [*HwScsiFindAdapter*](/previous-versions/windows/hardware/drivers/ff557300(v=vs.85)) 设置 [**端口 \_ 配置 \_ 信息**](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)时所指示的那样，端口驱动程序会在未完成请求超时时请求设备重置。

系统端口驱动程序使用 SRB 调用微型端口驱动程序的 *HwScsiStartIo* 例程，其中 **函数** 成员设置为 SRB \_ 函数 \_ 重置 \_ 设备。 微型端口驱动程序负责完成收到重置设备请求时设备上未完成的任何请求。

如果设备重置失败或超时，或者当端口驱动程序等待 **NextRequest** 通知时发生超时，则端口驱动程序将调用 [*HwScsiResetBus*](/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))。

 

