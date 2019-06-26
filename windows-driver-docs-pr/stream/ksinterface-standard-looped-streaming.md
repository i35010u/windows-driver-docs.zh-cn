---
title: KSINTERFACE\_标准\_LOOPED\_流式处理
description: KSINTERFACE\_标准\_LOOPED\_流式处理
ms.assetid: c12e7085-fa13-48d3-b4ed-ea0a708f026b
keywords:
- KSINTERFACE_STANDARD_LOOPED_STREAMING 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_LOOPED_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d039d627f30716ed36828e45b65c531cadc9b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370438"
---
# <a name="ksinterfacestandardloopedstreaming"></a>KSINTERFACE\_标准\_LOOPED\_流式处理


## <span id="ddk_ksinterface_standard_looped_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_LOOPED_STREAMING_KS"></span>


KSINTERFACE\_标准\_LOOPED\_DSound 的客户端使用流式处理接口。 在 Windows XP 的发布时，Kmixer 和 Portcls 是支持此接口的唯一 KS 音频筛选器。

如果 pin 支持 KSINTERFACE\_标准\_LOOPED\_流式处理相关的筛选器才会完成缓冲区 pin 将被置于*停止*状态。 通过连续循环围绕单个缓冲区中的数据筛选器处理数据提交到筛选器。

### <a name="see-also"></a>请参阅

[KSINTERFACESETID\_标准](ksinterfacesetid-standard.md)， [ **KSPIN\_接口**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))， [ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)

 

 





