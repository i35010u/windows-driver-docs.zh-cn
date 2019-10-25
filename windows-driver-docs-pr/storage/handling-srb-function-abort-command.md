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
ms.openlocfilehash: e606be54c4d7d450fc97a39058b21866f2dd0ec7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826262"
---
# <a name="handling-srb_function_abort_command"></a>处理 SRB\_函数\_中止\_命令


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


*HwScsiStartIo*例程还负责处理传入的 SRBs，并将**函数**成员设置为 SRB\_函数\_ABORT\_命令。

对于中止请求，微型端口驱动程序的*HwScsiStartIo*例程应该验证是否已通过调用目标逻辑单元的**ScsiPortGetSrb** ，并将返回的指针与当前 SRB 的**NextSrb**值。 如果它们不相等，则当前 SRB 已中止，微型端口驱动程序的*HwScsiStartIo*例程应执行以下操作：

1.  将输入 SRB 的**SrbStatus**设置为 SRB\_状态\_中止\_失败。

2.  用_NotificationType_**REQUESTCOMPLETE**和输入 SRB 调用[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与_NotificationType_**NextRequest**或**NextLuRequest**一起调用**ScsiPortNotification** 。

否则， *HwScsiStartIo*例程会执行以下操作：

1.  为请求在其设备、逻辑单元和/或 SRB 扩展中设置上下文。

2.  程序 HBA 中止给定的**NextSrb**请求。

 

 




