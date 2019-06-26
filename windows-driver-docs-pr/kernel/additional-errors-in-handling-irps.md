---
title: 处理 IRP 时出现其他错误
description: 处理 IRP 时出现其他错误
ms.assetid: fb46e7a8-8181-46d3-a929-cec01fd71f20
keywords:
- 可靠性 WDK 内核，双完成 Irp
- 双完成 Irp WDK 内核
- 丢失的 Irp WDK 内核
- 可靠性 WDK 内核丢失 Irp
- 聚合 IOCTL 公共和专用 IOCTL 路径
- 可靠性 WDK 内核聚合公钥和私钥 IOCTL 路径
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a5ab2ebffd9c0dd4b3a9d64f73fbf60e5cf47f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369993"
---
# <a name="additional-errors-in-handling-irps"></a>处理 IRP 时出现其他错误





以下是其他驱动程序，有时会做出处理 Irp 时的错误。

### <a name="lost-or-double-completed-irps"></a>丢失或双完成 Irp

这些问题以及缺少对 I/O 管理器例程的调用，如[ **IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)，通常出现在错误处理路径中。 驱动程序路径的快速评审可以找到此类问题。

### <a name="converging-public-ioctl-and-private-ioctl-paths"></a>聚合 IOCTL 公共和专用 IOCTL 路径

作为一般规则，驱动程序应为公共和专用 Ioctl （或 FSCTLs） 包含单独的执行路径。 驱动程序无法确定是否 IOCTL 或 FSCTL 请求是在内核模式或用户模式下查看控制代码。 因此，处理相同的执行路径中的公共和专用代码 （或执行最小的验证，然后再调用的相同例程） 可以打开安全漏洞的驱动程序。 如果专用 IOCTL 或 FSCTL 一项特权，知道控制代码的非特权的用户可能能够对其进行访问。 因此，如果您的驱动程序支持专用 IOCTL 或 FSCTL 请求，请确保它处理独立于任何公共 Ioctl 或 FSCTLs 还必须支持此类请求。

 

 




