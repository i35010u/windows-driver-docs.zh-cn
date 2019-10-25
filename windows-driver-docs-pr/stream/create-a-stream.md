---
title: 创建流
description: 创建流
ms.assetid: 9984275f-7ead-4df2-aa98-a3b4e5e85ae0
keywords:
- Avcstrm 流式处理筛选器驱动程序 WDK，创建流
- 流创建 WDK AV/C 流式处理
- 上下文 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3191e828bda2a6a26a0ea11c1e590d586ae4058
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827125"
---
# <a name="create-a-stream"></a>创建流





在 AV/C 流式处理筛选器驱动程序（ *Avcstrm*）可以提供服务之前，必须先创建数据流上下文。 上下文指向包含请求的数据格式、数据流状态和属性的不透明结构，类似于流扩展。 数据格式结构和数据流的方向是其输入参数。 如果可以成功创建流，它将返回流上下文。 此上下文由子单位驱动程序缓存，并用于后续 AV/C 流式处理请求。

这是一个同步操作。 操作首先创建流请求结构以打开流。 然后，它调用用户定义的 IRP 同步例程来调用低级驱动程序，以根据给定的数据流方向和在\_AVCSTRM 中定义的数据格式（ [ **\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)）创建数据流。 下面的代码示例演示了如何打开数据流上下文。

```cpp
#include <avcstrm.h>

INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_OPEN);
pAVCStrmReq->CommandData.OpenStruct.AVCFormatInfo =            &AVCStrmFormatInfoTable[pDevExt->VideoFormatIndex]; 
pAVCStrmReq->CommandData.OpenStruct.AVCStreamContext = NULL;
pAVCStrmReq->CommandData.OpenStruct.DataFlow         = DataFlow;

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );

if(STATUS_SUCCESS == Status) {
    // Save the context, which is used for a 
    // Subsequent call to the AVCStrm filter driver    
    pStrmExt->AVCStreamContext = 
        pAVCStrmReq->CommandData.OpenStruct.AVCStreamContext;
}
```

 

 




