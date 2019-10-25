---
title: SerCx2 对读取和写入请求的处理
description: 外设驱动程序将写入（IRP_MJ_WRITE）和读取（IRP_MJ_READ）请求发送到串行控制器上的端口，以便将数据传入和传出连接到该端口的外围设备。
ms.assetid: 98100680-7D27-42B7-A445-C539B2DF95AD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 283ff84025de76b66ad6eacfa18354232435adb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843048"
---
# <a name="sercx2-handling-of-read-and-write-requests"></a>SerCx2 对读取和写入请求的处理


外设驱动程序向串行控制器上的端口发送写入（[**irp\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))）并读取（[**irp\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))）请求，以将数据传入和传出连接到该端口的外围设备。 SerCx2 处理这些请求的方式经过良好定义，即使请求超时或被取消。

## <a name="cancellation-of-a-read-or-write-request"></a>取消读取或写入请求


在读取或写入请求完成之前，此请求可能会被操作系统或发送请求的外围驱动程序取消。 如果在 SerCx2 传输请求的任何数据之前发生取消，则 SerCx2 将完成状态为\_"已取消" 状态代码的请求。

但是，如果在为请求传输一个或多个字节的数据之后，但在传输请求的所有数据之前取消了读取或写入请求，则 SerCx2 会完成请求，状态\_成功状态代码。 完成的请求报告在处理请求的过程中由 SerCx2 读取或写入的字节数。 如果需要，发送请求的外围设备驱动程序可以使用此信息发送第二个请求以完成部分完成的读取或写入操作。

## <a name="requests-that-time-out"></a>请求超时


如果请求的处理时间过长，读取或写入请求可能会超时。 此外，如果串行控制器收到两个连续字节之间的时间超过了允许的最大时间，则读取请求可能会超时。 在任一情况下，如果检测到超时条件，SerCx2 会立即完成状态为\_超时状态代码的请求。 完成的请求报告在处理请求的过程中由 SerCx2 读取或写入的字节数。 如果需要，发送请求的外围设备驱动程序可以使用此信息发送第二个请求以完成部分完成的读取或写入操作。 有关超时的详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。

## <a name="impact-of-hardware-limitations"></a>硬件限制的影响


通常，SerCx2 会准确报告读取或写入请求所传输的字节数，超出或被取消。 但是，某些用于执行系统 DMA 事务的硬件可能无法准确地统计由部分完成的读取或写入事务传输的字节数。 如果是这样，则关联的读取或写入请求可能仅报告传输的字节数的近似值。

## <a name="requests-to-transfer-zero-bytes"></a>请求传输零字节


为了响应读取或写入请求以传输零字节，SerCx2 完成请求，状态\_成功状态代码，但不执行任何操作。

 

 




