---
title: Storport 微型端口驱动程序中的错误处理
description: Storport 微型端口驱动程序中的错误处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 001e150f962e6c552d6607e5fafa62203c0a5a76
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804633"
---
# <a name="error-handling-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的错误处理


每个 Storport 微型端口驱动程序必须通知系统端口驱动程序以下类型的 SCSI 错误。 应在 **SrbStatus** 成员中设置这些错误，然后驱动程序才能完成发生错误时正在处理的 SRB：

-   \_ \_ 如果 HBA 返回非特定总线错误，则 (SRB 状态错误) 

-   SRB \_ 状态 \_ 奇偶校验 \_ 错误

-   SRB \_ 状态 \_ 意外的 \_ 总线 \_ 可用

-   SRB \_ 状态 \_ 选择 \_ 超时

-   SRB \_ 状态 \_ 命令 \_ 超时

-   已 \_ 拒绝 SRB 状态 \_ 消息 \_

-   SRB \_ 状态 \_ 无 \_ 设备

-   SRB \_ 状态 \_ 无 \_ HBA

-   SRB \_ 状态 \_ 数据 \_ 超限 (也为不足) 返回

-   SRB \_ 状态 \_ 阶段 \_ 序列 \_ 失败

-   SRB \_ 状态 \_ (TID 繁忙) 

对于数据不足，微型端口驱动程序必须更新 SRB 的 **DataTransferLength** ，以指示实际传输的数据量。

此外，小型端口驱动程序应使用以下准则来记录前面的一些错误，方法是将 SRB 传递到 [**StorPortLogError**](/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)：

记录 SRB 状态错误的驱动程序编写器错误 \_ \_ 。

对于 SRB \_ 状态 \_ 奇偶校验错误始终记录错误 \_ 。

对于 SRB 状态 "意外的 \_ \_ \_ 总线可用"，始终记录错误 \_ 。

对于 SRB \_ 状态选择超时，始终记录错误 \_ \_ 。

对于 SRB \_ 状态命令超时，始终记录错误 \_ \_ 。

\_ \_ \_ 每当发生溢出但未发生不足时，记录 SRB 状态数据溢出的错误。

对于 SRB \_ 状态 \_ 阶段 \_ 序列失败，始终记录错误 \_ 。

对于硬件错误，总是记录 SRB 状态的错误 \_ \_ 。

若要记录错误，微型端口驱动程序使用以下系统定义的错误或警告代码之一调用 [**StorPortLogError**](/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror) ：

SP \_ 总线 \_ 奇偶校验 \_ 错误映射到 SRB \_ 状态 \_ 奇偶校验 \_ 错误

\_ \_ 目标逻辑单元 (的 SP 意外断开连接) 

SP \_ 无效 \_ RESELECTION 映射到 SRB \_ 状态 \_ 阶段 \_ 序列 \_ 失败或 SRB \_ 状态 \_ 错误

SP \_ 总线 \_ 超时 \_ 映射到 SRB \_ 状态 \_ 选择 \_ 超时

SP \_ 请求 \_ 超时映射到 SRB \_ 状态 \_ 命令 \_ 超时

SP \_ 协议 \_ 错误映射到 SRB \_ 状态 \_ 阶段 \_ 选择 \_ 失败，SRB \_ 状态 \_ 意外 \_ \_ 的可用总线，或 \_ \_ \_ 针对超限情况 SRB 状态数据溢出

SP \_ 内部 \_ 适配器 \_ 错误映射到 SRB \_ 状态 \_ 错误

SP \_ IRQ \_ 未 \_ 响应 (警告微型端口驱动程序已检测到 HBA 不再产生中断请求) 

SP \_ 错误 \_ fw \_ 错误，其中 fw 是 *固件*) 

SP \_ 错误 \_ FW \_ 警告

[**StorPortLogError**](/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror) 分配错误日志数据包，对其进行设置，并在代表微型端口驱动程序的事件日志中记录 i/o 错误。 系统管理员或用户可以通过检查系统事件日志，并在必要时重新配置、修复或更换 HBA 来监视 HBA 的状况。

 

