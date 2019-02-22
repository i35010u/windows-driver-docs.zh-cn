---
title: SerCx2 处理读取和写入请求
description: 外围设备驱动程序将写入 (IRP_MJ_WRITE) 和读取 (IRP_MJ_READ) 请求发送到传输数据传入和传出连接到端口的外围设备的串行控制器上的端口。
ms.assetid: 98100680-7D27-42B7-A445-C539B2DF95AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e71adc20a8da60c2a600f5aa4fcc43810ab84b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543255"
---
# <a name="sercx2-handling-of-read-and-write-requests"></a>SerCx2 处理读取和写入请求


外围设备的驱动程序将发送写入 ([**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 和读取 ([**IRP\_MJ\_读取** ](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 串行控制器上的端口的请求来传输数据传入和传出外围设备连接到的端口。 在其中 SerCx2 处理这些请求的方式是有明确定义，即使请求超时或被取消。

## <a name="cancellation-of-a-read-or-write-request"></a>取消的读或写请求


读或写请求完成之前，由操作系统或将请求发送的外围设备驱动程序可能会取消此请求。 如果取消发生之前 SerCx2 传输请求的任何数据，SerCx2 完成时的状态请求\_已取消状态代码。

但是，如果后一个或多个字节的数据传输请求，但在之前的所有数据的传输请求已取消读取或写入请求，SerCx2 完成的状态请求\_成功状态代码。 已完成的请求报告读取或写入请求的处理期间的 SerCx2 的字节的数。 如有必要，将请求发送的外围设备驱动程序可以使用此信息发送完成部分完成的读 / 写操作的第二个请求。

## <a name="requests-that-time-out"></a>请求时超时


如果读取或写入请求可能超时，如果请求花费太长，无法处理。 此外，读取的请求可能超时，如果接收到的串行控制器的两个连续字节之间的时间超过了一些最大允许的时间。 在任一情况下，检测到的超时条件时，SerCx2 立即完成请求的状态\_超时状态代码。 已完成的请求报告读取或写入请求的处理期间的 SerCx2 的字节的数。 如有必要，将请求发送的外围设备驱动程序可以使用此信息发送完成部分完成的读 / 写操作的第二个请求。 有关超时的详细信息，请参阅[**串行\_超时**](https://msdn.microsoft.com/library/windows/hardware/hh439614)。

## <a name="impact-of-hardware-limitations"></a>硬件限制的影响


通常情况下，SerCx2 准确地报告由超时或已取消的读或写请求传输的字节数。 但是，某些硬件用于执行系统 DMA 事务可能不准确计数部分完成的读取或写入事务传输的字节数。 如果是这样，关联的读取或写入请求可能会报告仅传输的字节数的近似计数。

## <a name="requests-to-transfer-zero-bytes"></a>将零字节的请求


对传输零字节的读取或写入请求的响应，SerCx2 完成状态请求\_成功状态代码但不执行任何操作。

 

 




