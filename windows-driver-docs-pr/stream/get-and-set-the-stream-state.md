---
title: 获取和设置流状态
description: 获取和设置流状态
keywords:
- Avcstrm.sys 流筛选器驱动程序 WDK，流状态
- 流状态 WDK AV/C 流式处理
- 状态 WDK AV/C 流式处理
- KSSTATE_STOP
- KSSTATE_ACQUIRE
- KSSTATE_PAUSE
- KSSTATE_RUN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c1308d3a3cd0df9042e8dea3b10c02d94b20e76
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815835"
---
# <a name="get-and-set-the-stream-state"></a>获取和设置流状态





子单位接收来自客户端应用程序的 IOCTLs，以获取当前流状态或设置为新的流状态。 创建数据流时，会将其初始化为 **KSSTATE \_ 停止** 状态。 按 **KSSTATE \_ 获取** 状态分配同步资源，如果该资源失败，则将返回 \_ \_ " **KSSTATE \_ 暂停**" 状态下的 *Ntstatus*) 中声明的 " (资源不足" 的状态。 数据流将在 **KSSTATE \_ 运行** 状态中开始。

下面的代码示例将流设置为新状态：

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_SET_STATE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext; //  From cached context saved in OPEN_STREAM request
pAVCStrmReq->CommandData.StreamState = StreamState; // New stream state

Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );
```

下面的代码示例查询当前流状态：

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_GET_STATE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request

Status = 
    AVCStrmReqSubmitIrpSynch( 
        DeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );

// If return STATUS_SUCCESS, the current stream state is in
// pAVCStrmReq->CommandData.StreamState 
```

 

 




