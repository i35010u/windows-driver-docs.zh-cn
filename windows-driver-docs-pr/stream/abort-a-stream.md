---
title: 中止流
description: 中止流
keywords:
- Avcstrm.sys 流筛选器驱动程序 WDK，中止流
- 中止流 WDK AV/C 流式处理
- 停止流式处理 WDK AV/C 流式处理
- 流中止 WDK AV/C 流式处理
- 取消流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21decf7e4029ec152fb0895a0f7efabf889b2b83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790305"
---
# <a name="abort-a-stream"></a>中止流





当某个子单位遇到特殊条件时，如设备删除或流数据 IOCTL 取消时，应中止流式处理操作。 中止操作 *请求* 是同步的，但中止完成不是。 仅接受并处理第一个中止流请求;将忽略重复的请求，但会返回状态 " \_ 成功"。 AV/C 流式处理筛选器驱动程序 *Avcstrm.sys，* 然后计划一个工作项以中止流式处理。 当流中止时，它将开始完成 [**AVCSTRM \_ READ**](./avcstrm-read.md) / [**AVCSTRM \_ WRITE**](./avcstrm-write.md)请求，状态为 "已 \_ 取消"。 流状态不会随中止请求而更改，必须关闭数据流才能清理和释放资源。

在 "中止工作项" 例程中，AV/C 流式处理将首先停止同步数据传输，但不会影响流状态。 然后，AV/C 流式处理会经历附加的流数据队列，以分离流缓冲区并返回状态为 "已取消" 的流 \_ 。

若要发出此请求，将使用 **AVCSTRM \_ 中止 \_ 流式处理** 请求和数据流上下文初始化 AV/C 流式处理请求。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_ABORT_STREAMING);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pStrmExt->pDevExt->pBusDeviceObject,
        pStrmExt->pIrpAbort,
        pAVCStrmReq
        );
```

当数据流中止时，如果未) 删除该设备的流状态，则可以将其恢复 (如果其客户端应用程序 **\_ 停止了 KSSTATE** 。

 

