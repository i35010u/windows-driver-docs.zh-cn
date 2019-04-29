---
title: 创建流
description: 创建流
ms.assetid: 9984275f-7ead-4df2-aa98-a3b4e5e85ae0
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK、 创建流
- 流创建 WDK AV/C 流式处理
- 上下文 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e465d05ce37b2c9e15efe02d589a04983eae3d8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374173"
---
# <a name="create-a-stream"></a>创建流





AV/C 流式处理筛选器驱动程序之前，必须创建数据的流上下文*Avcstrm.sys*，可以提供服务。 上下文是指向包含请求的数据格式、 数据流状态和属性，类似于流扩展的不透明结构。 数据格式结构和数据流的方向是其输入的参数。 如果可以成功创建流，它将返回的流上下文。 此上下文中缓存的子单元驱动程序，并用于后续 AV/C 流式处理请求。

这是一项同步操作。 此操作会首先创建的流请求结构，以打开一个流。 然后，它调用的用户定义 IRP 同步例程以调用较低的驱动程序来创建基于给定的数据流方向和中定义的数据格式的数据流[ **AVCSTRM\_格式\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554117). 下面的代码示例演示如何打开数据的流上下文。

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

 

 




