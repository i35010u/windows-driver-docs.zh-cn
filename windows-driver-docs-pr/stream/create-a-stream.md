---
title: 创建流
description: 创建流
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK，创建流
- 流创建 WDK AV/C 流式处理
- 上下文 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 293eb2c9321f453f2c3840d59adb7777acf79019
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811393"
---
# <a name="create-a-stream"></a>创建流





在 AV/C 流式处理筛选器驱动程序 *Avcstrm.sys* 可以提供服务之前，必须创建数据流上下文。 上下文指向包含请求的数据格式、数据流状态和属性的不透明结构，类似于流扩展。 数据格式结构和数据流的方向是其输入参数。 如果可以成功创建流，它将返回流上下文。 此上下文由子单位驱动程序缓存，并用于后续 AV/C 流式处理请求。

这是一个同步操作。 操作首先创建流请求结构以打开流。 然后，它调用用户定义的 IRP 同步例程来调用低级驱动程序，以创建基于给定数据流方向和在 [**AVCSTRM \_ 格式 \_ 信息**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)中定义的数据格式的数据流。 下面的代码示例演示了如何打开数据流上下文。

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

 

