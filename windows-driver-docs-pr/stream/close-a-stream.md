---
title: 关闭流
description: 关闭流
ms.assetid: 1ed9b07c-8d22-485f-a7e8-3a27ca3768b0
keywords:
- Avcstrm.sys 流式处理筛选器驱动程序 WDK、 关闭流
- 关闭 WDK AV/C 流式处理流
- 关闭流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6713a9e053d918b2569663ac7b0e9ae24b8e9ff3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372360"
---
# <a name="close-a-stream"></a>关闭流

流操作完成后，必须关闭该数据流来释放所分配的打开的流请求的资源。

如果流*状态*不会停止运行或没有挂起的 I/O，关闭流请求将完成数据请求，并将 IRP 的状态设置为状态\_已取消。

```cpp
INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_CLOSE);
pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;  // From cached context saved in OPEN_STREAM request
Status = 
    AVCStrmReqSubmitIrpSynch( 
        pDevExt->pBusDeviceObject,
        pStrmExt->pIrpReq,
        pAVCStrmReq
        );
```
