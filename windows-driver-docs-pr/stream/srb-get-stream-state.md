---
title: SRB \_ 获取 \_ 流 \_ 状态
description: SRB \_ 获取 \_ 流 \_ 状态
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c3e927bf040ed67903e13b2a78e35aa3203aff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803449"
---
# <a name="srb_get_stream_state"></a>SRB \_ 获取 \_ 流 \_ 状态


## <span id="ddk_srb_get_stream_state_ks"></span><span id="DDK_SRB_GET_STREAM_STATE_KS"></span>


类驱动程序发送此请求以获取此流的流状态。 微型驱动程序进入 *pSrb* - &gt; **CommandData** 中的流状态。**StreamState**。 有关流状态的说明，请参阅 [**KSPROPERTY \_ 连接 \_ 状态**](ksproperty-connection-state.md) 。

 

 





