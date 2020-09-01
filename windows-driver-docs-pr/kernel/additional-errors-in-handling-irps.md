---
title: 处理 IRP 时出现其他错误
description: 处理 IRP 时出现其他错误
ms.assetid: fb46e7a8-8181-46d3-a929-cec01fd71f20
keywords:
- 可靠性 WDK 内核，双完成 Irp
- 双完成 Irp WDK 内核
- 丢失 Irp WDK 内核
- 可靠性 WDK 内核，丢失 Irp
- 聚合公共 IOCTL 和私有 IOCTL 路径
- 可靠性 WDK 内核，聚合公共和专用 IOCTL 路径
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6d84e8928ebbee95f9bdf0f7fbbbd70624f37b7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192063"
---
# <a name="additional-errors-in-handling-irps"></a>处理 IRP 时出现其他错误





下面是驱动程序在处理 Irp 时有时会发生的其他错误。

### <a name="lost-or-double-completed-irps"></a>丢失或已完成的 Irp

这些问题以及缺少对 i/o 管理器例程（如 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)）的调用，通常出现在错误处理路径中。 快速查看驱动程序路径可发现此类问题。

### <a name="converging-public-ioctl-and-private-ioctl-paths"></a>聚合公共 IOCTL 和私有 IOCTL 路径

作为一般规则，驱动程序应包含公共和专用 IOCTLs (或 FSCTLs) 的单独执行路径。 驱动程序无法通过查看控件代码来确定 IOCTL 或 FSCTL 请求是源自内核模式还是用户模式。 因此，处理同一执行路径中的公共和私有代码 (或执行最小验证，然后调用相同的例程) 可以打开安全漏洞驱动程序。 如果私有 IOCTL 或 FSCTL 有特权，则知道控制代码的非特权用户可能能够访问它。 因此，如果你的驱动程序支持专用 IOCTL 或 FSCTL 请求，请确保它在它还必须支持的任何公共 IOCTLs 或 FSCTLs 上分别处理此类请求。

 

