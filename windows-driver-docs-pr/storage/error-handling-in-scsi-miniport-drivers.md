---
title: SCSI 微型端口驱动程序中的错误处理
description: SCSI 微型端口驱动程序中的错误处理
ms.assetid: 0d9a2d60-c8e5-48f6-9c1f-d593e59095c8
keywords:
- SCSI 微型端口驱动程序 WDK 存储，错误
- 错误 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7044e0563a47926a7267090329c52d83e1399923
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844556"
---
# <a name="error-handling-in-scsi-miniport-drivers"></a>SCSI 微型端口驱动程序中的错误处理


## <span id="ddk_error_handling_in_scsi_miniport_drivers_kg"></span><span id="DDK_ERROR_HANDLING_IN_SCSI_MINIPORT_DRIVERS_KG"></span>


每个 SCSI 微型端口驱动程序必须通知系统端口驱动程序以下类型的 SCSI 错误。 应在**SrbStatus**成员中设置这些错误，然后驱动程序才能完成发生错误时正在处理的 SRB：

-   SRB\_状态\_错误（如果 HBA 返回非特定总线错误）

-   SRB\_状态\_奇偶校验\_错误

-   SRB\_状态\_意外\_总线\_免费

-   SRB\_状态\_选择\_超时

-   SRB\_状态\_命令\_超时

-   已拒绝 SRB\_状态\_消息\_

-   SRB\_状态\_无\_设备

-   SRB\_状态\_无\_HBA

-   SRB\_状态\_数据\_超限（也为不足返回）

-   SRB\_状态\_阶段\_序列\_故障

-   SRB\_状态\_繁忙（TID 繁忙）

对于数据不足，微型端口驱动程序必须更新 SRB 的**DataTransferLength** ，以指示实际传输的数据量。

此外，小型端口驱动程序应使用以下准则来记录前面的一些错误，方法是将 SRB 传递到[**ScsiPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror)：

记录 SRB 的驱动程序编写器\_状态\_错误的错误消息。

对于 SRB\_状态始终记录错误\_奇偶校验\_错误。

始终记录 SRB\_状态的错误\_意外\_总线\_免费。

对于 SRB\_状态\_选择\_超时，始终记录错误。

始终记录 SRB\_状态的错误\_命令\_超时。

在发生溢出时，记录 SRB\_状态的错误\_数据\_超限，但不记录发生不足的情况。

对于 SRB\_状态应始终记录错误\_阶段\_序列\_失败。

对于出现硬件错误\_繁忙\_状态，请始终记录错误。

若要记录错误，微型端口驱动程序使用以下系统定义的错误或警告代码之一调用[**ScsiPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror) ：

SP\_总线\_奇偶校验\_错误映射到 SRB\_状态\_奇偶校验\_错误

SP\_意外\_断开连接（由目标逻辑单元）

SP\_无效\_RESELECTION 映射到 SRB\_状态\_阶段\_序列\_失败或 SRB\_状态\_错误

SP\_总线\_时间\_OUT 映射到 SRB\_状态\_选择\_超时

SP\_请求\_超时映射到 SRB\_状态\_命令\_超时

SP\_协议\_错误映射到 SRB\_状态\_阶段\_选择\_失败，SRB\_状态\_意外\_总线\_可用或 SRB\_状态\_数据超限条件\_超限

SP\_内部\_适配器\_错误映射到 SRB\_状态\_错误

SP\_IRQ\_不\_响应（警告微型端口驱动程序已检测到 HBA 不再产生中断请求）

SP\_错误\_固件\_错误（FW 是*固件*）

SP\_错误\_固件\_警告

[**ScsiPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportlogerror)分配错误日志数据包，对其进行设置，并在代表微型端口驱动程序的事件日志中记录 i/o 错误。 系统管理员或用户可以通过检查系统事件日志，并在必要时重新配置、修复或更换 HBA 来监视 HBA 的状况。

 

 




