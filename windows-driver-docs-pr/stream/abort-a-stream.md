---
title: 中止流
description: 中止流
ms.assetid: 46c726b6-8553-4588-9be1-2cf7779efec5
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK，正在中止流
- 中止流 WDK AV/C 流式处理
- 停止流式处理 WDK AV/C 流式处理
- 流中止 WDK AV/C 流式处理
- 正在取消流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48ec5181a900d67261bb34f235729d5d1f2bee4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357223"
---
# <a name="abort-a-stream"></a>中止流





子单元遇到特殊情况，例如设备删除或流数据 IOCTL 取消时应中止流式处理操作。 中止操作*请求*是同步的但不是中止完成。 接受和处理，则只有第一个中止流请求重复请求将被忽略，但返回带有状态\_成功。 AV/C 流式处理筛选器驱动程序*Avcstrm.sys，* 然后安排要中止流式处理的工作项。 当流传输中止时，它开始完成[ **AVCSTRM\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff554130)/[**AVCSTRM\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff554135)状态请求\_已取消。 流状态未更改与中止请求，并且数据流仍必须关闭清理并释放资源。

在中止工作项例程中，C AV/流式处理将首先停止同步数据传输，但它不会影响流状态。 AV/C 流式处理然后经历附加的流数据队列来分离流缓冲区，并将其返回带有状态\_已取消。

若要发出此请求，AV/C 流式处理的请求初始化**AVCSTRM\_中止\_流式处理**请求和数据的流上下文。

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

当中止的数据流时，它 （如果设备未被删除） 后，可继续其流状态重置为**KSSTATE\_停止**其客户端应用程序。

 

 




