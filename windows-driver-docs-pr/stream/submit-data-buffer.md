---
title: 提交数据缓冲区
description: 提交数据缓冲区
keywords:
- Avcstrm.sys 流筛选器驱动程序 WDK，数据缓冲区提交
- 数据缓冲区 WDK AV/C 流式处理
- 提交数据缓冲区 WDK AV/C 流式处理
- 缓冲 WDK AV/C 流式处理
- 挂起流 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d3b9132ebde93e3805111bcc4eade018c1974ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839835"
---
# <a name="submit-data-buffer"></a>提交数据缓冲区





使用打开流时，子单位驱动程序可以开始将流样本附加到 AV/C 流式处理。 这些示例可以是读取或写入操作，并且可以通过与 AV/C 流式处理筛选器驱动程序相同的方式提交 *Avcstrm.sys*。 此服务始终是异步的，因为它依赖于当前流状态和流数据可用性。

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

由于操作是异步的，因此状态应为 " \_ 挂起"。 数据完成后，将调用完成例程。 在完成例程中，子单位驱动程序可以执行后处理，包括更新处理的数据的统计信息，并且在子单位为时钟提供程序时可能会增加演示时间。

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
