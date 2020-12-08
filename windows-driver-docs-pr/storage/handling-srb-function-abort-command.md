---
title: 处理 SRB_FUNCTION_ABORT_COMMAND
description: 处理 SRB_FUNCTION_ABORT_COMMAND
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_ABORT_COMMAND
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fd3a1eb47751defb531fb1aa2ffc1f2616ea6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835217"
---
# <a name="handling-srb_function_abort_command"></a>处理 SRB \_ FUNCTION \_ ABORT \_ 命令


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


*HwScsiStartIo* 例程还负责处理传入的 SRBs，并将 **函数** 成员设置为 SRB \_ 函数 \_ ABORT \_ 命令。

对于中止请求，微型端口驱动程序的 *HwScsiStartIo* 例程应该验证是否已通过对目标逻辑单元调用 **ScsiPortGetSrb** 并将返回的指针与当前 SRB 的 **NextSrb** 值进行比较来中止给定的 SRB。 如果它们不相等，则当前 SRB 已中止，微型端口驱动程序的 *HwScsiStartIo* 例程应执行以下操作：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ 状态 \_ 中止 \_ 失败。

2.  用 _NotificationType_**REQUESTCOMPLETE** 和输入 SRB 调用 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与 _NotificationType_**NextRequest** 或 **NextLuRequest** 一起调用 **ScsiPortNotification** 。

否则， *HwScsiStartIo* 例程会执行以下操作：

1.  为请求在其设备、逻辑单元和/或 SRB 扩展中设置上下文。

2.  程序 HBA 中止给定的 **NextSrb** 请求。

 

