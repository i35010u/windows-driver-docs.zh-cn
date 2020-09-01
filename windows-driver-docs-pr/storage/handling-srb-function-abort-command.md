---
title: 处理 SRB_FUNCTION_ABORT_COMMAND
description: 处理 SRB_FUNCTION_ABORT_COMMAND
ms.assetid: 74d46df6-2e3e-45d8-bedb-a81a80a0aec1
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_ABORT_COMMAND
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d9b9604359b074fc1f7354539a9d6926c222c44
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184207"
---
# <a name="handling-srb_function_abort_command"></a>处理 SRB \_ FUNCTION \_ ABORT \_ 命令


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


*HwScsiStartIo*例程还负责处理传入的 SRBs，并将**函数**成员设置为 SRB \_ 函数 \_ ABORT \_ 命令。

对于中止请求，微型端口驱动程序的 *HwScsiStartIo* 例程应该验证是否已通过对目标逻辑单元调用 **ScsiPortGetSrb** 并将返回的指针与当前 SRB 的 **NextSrb** 值进行比较来中止给定的 SRB。 如果它们不相等，则当前 SRB 已中止，微型端口驱动程序的 *HwScsiStartIo* 例程应执行以下操作：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ 状态 \_ 中止 \_ 失败。

2.  用_NotificationType_**REQUESTCOMPLETE**和输入 SRB 调用[**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与_NotificationType_**NextRequest**或**NextLuRequest**一起调用**ScsiPortNotification** 。

否则， *HwScsiStartIo* 例程会执行以下操作：

1.  为请求在其设备、逻辑单元和/或 SRB 扩展中设置上下文。

2.  程序 HBA 中止给定的 **NextSrb** 请求。

 

