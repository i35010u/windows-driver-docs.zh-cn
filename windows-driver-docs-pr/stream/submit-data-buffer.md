---
title: 提交数据缓冲区
description: 提交数据缓冲区
ms.assetid: 151f5139-3706-4255-9d71-d8e6e3416b7c
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK，数据缓冲提交
- 数据缓冲 WDK AV/C 流式处理
- 提交数据缓冲区 WDK AV/C 进行流式处理
- 缓冲 WDK AV/C 流式处理
- 挂起的流式处理 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9da43ed6acf278b3ce8ee402e75f0b2206fb3c89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390867"
---
# <a name="submit-data-buffer"></a>提交数据缓冲区





与打开流，可以开始的子单元驱动程序将附加到 AV/C 流式处理流示例。 这些示例可以既读取或写入操作，并可将其提交到 AV/C 流式处理筛选器驱动程序，相同的方式*Avcstrm.sys*。 此服务是始终异步因为其对当前的流状态和流数据可用性的依赖关系。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, (pSrb->Command == SRB_READ_DATA) ?      <mark type="enumval">AVCSTRM_READ</mark> : AVCSTRM_WRITE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // from cached context saved in OPEN_STREAM request

// Avcstrm.sys does not act as a clock provider. The subunit driver must provide this functionality if it wants to be the clock provider.

pAVCStrmReq->CommandData.BufferStruct.StreamHeader = pSrb->CommandData.DataBufferArray;

pAVCStrmReq->CommandData.BufferStruct.FrameBuffer =             
MmGetSystemAddressForMdlSafe(pSrb->Irp->MdlAddress,          NormalPagePriority);

// This is an asynchronous operation
NextIrpStack = IoGetNextIrpStackLocation(pIrpReq);
NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_AVCSTRM_CLASS;
NextIrpStack->Parameters.Others.Argument1 = pAVCStrmReq;

// Cannot be canceled! Use <mark type="enumval">AVCSTRM_ABORT_STREAMING</mark> to abort
IoSetCancelRoutine(
    pIrpReq,
    NULL
    );

IoSetCompletionRoutine( 
    pIrpReq,
    AVCTapeReqReadDataCR,
    pDriverReq,
    TRUE,  // Success
    TRUE,  // Error
    TRUE   // or Cancel
    );

pSrb->Status = STATUS_PENDING;

Status = 
    IoCallDriver(
        pDevExt->pBusDeviceObject,
        pIrpReq
        );
```

因为该操作是异步的状态应显示为状态\_PENDING。 完成数据后，将调用完成例程。 在完成例程，子单元驱动程序可以执行后续处理，包括更新处理的数据的统计信息和可能是仅当子单元是时钟提供程序添加呈现时间。

```cpp
// Keep track of the number of frames processed
pStrmExt->FramesProcessed++;

// Retrieve current stream time
if(pStrmExt->hMasterClock) 
    pStrmExt->CurrentStreamTime = pSrb->CommandData.DataBufferArray->PresentationTime.Time;

// Update final status
pSrb->Status = pIrpReq->IoStatus.Status;

// Complete this data SRB
StreamClassStreamNotification( 
    StreamRequestComplete,
    pSrb->StreamObject,
    pSrb 
    );
```
