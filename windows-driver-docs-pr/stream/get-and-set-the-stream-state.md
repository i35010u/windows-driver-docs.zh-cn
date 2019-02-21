---
title: 获取和设置 Stream 状态
description: 获取和设置 Stream 状态
ms.assetid: e2fde528-d0cf-4ffe-945a-8672b76db61f
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK，流状态
- 流状态 WDK AV/C 流式处理
- 指出 WDK AV/C 流式处理
- KSSTATE_STOP
- KSSTATE_ACQUIRE
- KSSTATE_PAUSE
- KSSTATE_RUN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914adb45fbc1fbcc7564abad60c63adb49a403f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521922"
---
# <a name="get-and-set-the-stream-state"></a>获取和设置 Stream 状态





子单元接收 Ioctl 从客户端应用程序以获取当前的流状态或将设置为新的流状态。 创建数据流后，它将初始化为**KSSTATE\_停止**状态。 等时的资源分配中**KSSTATE\_ACQUIRE**状态，并且如果失败，它将返回状态\_不足\_资源 (在中声明*Ntstatus.h*)在中**KSSTATE\_暂停**状态。 数据进行流式处理中将开始**KSSTATE\_运行**状态。

下面的代码示例设置为新状态的流：

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

当前的流状态的以下代码示例查询：

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

 

 




