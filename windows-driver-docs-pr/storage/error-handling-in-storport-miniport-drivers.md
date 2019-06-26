---
title: Storport 微型端口驱动程序中的错误处理
description: Storport 微型端口驱动程序中的错误处理
ms.assetid: 23ea8c36-56cf-45ae-a066-765d3a91b542
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66c33442cf327b37573a94c10198fcf60bc96bb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369575"
---
# <a name="error-handling-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的错误处理


每个 Storport 微型端口驱动程序必须通知以下类型的 SCSI 错误有关的系统端口驱动程序。 应在设置这些错误**SrbStatus**驱动程序完成其处理中出现错误 SRB 之前的成员：

-   SRB\_状态\_错误 （如果 HBA 返回一个非特定的总线错误）

-   SRB\_状态\_奇偶校验\_错误

-   SRB\_STATUS\_UNEXPECTED\_BUS\_FREE

-   SRB\_状态\_选择\_超时

-   SRB\_状态\_命令\_超时

-   SRB\_状态\_消息\_已拒绝

-   SRB\_状态\_否\_设备

-   SRB\_状态\_否\_HBA

-   SRB\_状态\_数据\_溢出 （还返回不足）

-   SRB\_状态\_阶段\_序列\_失败

-   SRB\_状态\_忙 (TID 忙)

对于数据不足，微型端口驱动程序必须更新 SRB **DataTransferLength**以指示实际传输数据量。

此外，微型端口驱动程序应使用以下准则来记录上述错误的一些通过将传递到 SRB [ **StorPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror):

记录裁量权 SRB 的驱动程序编写器的错误\_状态\_错误。

始终为 SRB 记录错误\_状态\_奇偶校验\_错误。

始终为 SRB 记录错误\_状态\_意外\_总线\_免费。

始终为 SRB 记录错误\_状态\_选择\_超时。

始终为 SRB 记录错误\_状态\_命令\_超时。

为 SRB 记录错误\_状态\_数据\_无论何时发生溢出，而不是在不足则会发生溢出。

始终为 SRB 记录错误\_状态\_阶段\_序列\_失败。

始终为 SRB 记录错误\_状态\_忙是否有硬件错误。

若要记录错误，微型端口驱动程序调用[ **StorPortLogError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)通过使用以下系统定义的错误或警告代码之一：

SP\_总线\_奇偶校验\_错误映射到 SRB\_状态\_奇偶校验\_错误

SP\_意外的\_断开连接 （通过目标逻辑单元）

SP\_无效\_此映射到 SRB\_状态\_阶段\_序列\_故障或 SRB\_状态\_错误

SP\_总线\_时间\_扩展映射到 SRB\_状态\_选择\_超时

SP\_请求\_超时值将映射到 SRB\_状态\_命令\_超时

SP\_协议\_错误映射到 SRB\_状态\_阶段\_选择\_失败、 SRB\_状态\_意外的\_总线\_免费版或 SRB\_状态\_数据\_溢出溢出条件

SP\_内部\_适配器\_错误映射到 SRB\_状态\_错误

SP\_IRQ\_不\_正在响应 （微型端口驱动程序已检测到 HBA 不再生成中断请求的警告）

SP\_坏\_转发\_转发的错误*固件*)

SP\_坏\_转发\_警告

[**StorPortLogError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)分配错误日志数据包，将其设置，并代表微型端口驱动程序在事件日志中记录的 I/O 错误。 系统管理员或用户可以通过检查系统事件日志并，如有必要，重新配置、 修复或出现故障之前更换 HBA 监视 HBA 的条件。

 

 




