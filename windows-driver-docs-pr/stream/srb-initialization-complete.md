---
title: SRB \_ 初始化 \_ 完成
description: SRB \_ 初始化 \_ 完成
ms.assetid: 72412ab0-226d-4bf6-af6b-98d62653e061
keywords:
- SRB_INITIALIZATION_COMPLETE 流媒体设备
topic_type:
- apiref
api_name:
- SRB_INITIALIZATION_COMPLETE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45bc3aac470eb2216560bffed2758eeee6fd82e3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190357"
---
# <a name="srb_initialization_complete"></a>SRB \_ 初始化 \_ 完成


## <span id="ddk_srb_initialization_complete_ks"></span><span id="DDK_SRB_INITIALIZATION_COMPLETE_KS"></span>


类驱动程序发送此请求，通知微型驱动程序已完成初始化。

### <a name="comments"></a>注释

微型驱动程序完成此请求后，类驱动程序可以开始发送 [**SRB 打开的 \_ \_ 流**](srb-open-stream.md) 请求。

如果微型驱动程序接收到此 SRB，微型驱动程序应创建任何必需的注册表项。 例如，DirectShow 过滤器可以使用 [**StreamClassRegisterFilterWithNoKSPins**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisterfilterwithnokspins) 例程注册电视调谐器或十字，以便与 FilterGraph 一起使用。

 

