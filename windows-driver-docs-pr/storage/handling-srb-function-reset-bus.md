---
title: 处理 SRB_FUNCTION_RESET_BUS
description: 处理 SRB_FUNCTION_RESET_BUS
ms.assetid: 285cbd5c-e364-4f0f-9020-0bc6f3d45cac
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_BUS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36999d92ae67de52f7d03c424d3be4ac4ee3cff
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190640"
---
# <a name="handling-srb_function_reset_bus"></a>处理 SRB \_ 函数 \_ 重置 \_ 总线


## <span id="ddk_handling_srb_function_reset_bus_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_BUS_KG"></span>


系统端口驱动程序始终将自己的重置总线请求直接发送到微型端口驱动程序的 [*HwScsiResetBus*](/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)) 例程，如 [SCSI 微型端口驱动程序的 HwScsiResetBus 例程](scsi-miniport-driver-s-hwscsiresetbus-routine.md)中所述。

但是， [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) **Function** \_ \_ \_ 如果基于 NT 的操作系统存储类驱动程序请求此操作，则可以使用 SRB 调用 HwScsiStartIo 例程，其中函数成员设置为 SRB 函数重置总线。 *HwScsiStartIo*例程只需调用*HwScsiResetBus*例程即可满足传入的总线重置请求。

 

