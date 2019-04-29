---
title: SRB\_GET\_STREAM\_STATE
description: SRB\_GET\_STREAM\_STATE
ms.assetid: ea868e5e-0724-4064-bccb-85d5b6e93d89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 225d2f870d2d5ccb7f0c1d94a73d73964ac211c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390862"
---
# <a name="srbgetstreamstate"></a>SRB\_GET\_STREAM\_STATE


## <span id="ddk_srb_get_stream_state_ks"></span><span id="DDK_SRB_GET_STREAM_STATE_KS"></span>


在类驱动程序将发送此请求以获取为此流的流状态。 微型驱动程序将进入流状态中的*pSrb*-&gt;**CommandData**。**StreamState**。 请参阅[ **KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)流状态的说明。

 

 





