---
title: 关闭流
description: 关闭流
keywords:
- Avcstrm.sys 流筛选器驱动程序 WDK，关闭流
- 流关闭 WDK AV/C 流式处理
- 正在关闭流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bb9cc0e0b0313ed6354adddcb26d028bcc656a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788183"
---
# <a name="close-a-stream"></a>关闭流

流操作完成后，必须关闭数据流才能释放由打开的流请求所分配的资源。

如果流 *状态* 不是 "已停止" 或正在等待 i/o，则关闭流请求将完成数据请求，并将 IRP 的状态设置为 "已 \_ 取消"。

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
