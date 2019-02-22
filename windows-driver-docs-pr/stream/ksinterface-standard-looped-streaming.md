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
ms.openlocfilehash: 2790708409e3ce9079d6c6329cc5043cb6a35fc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519552"
---
# <a name="ksinterfacestandardloopedstreaming"></a>KSINTERFACE\_标准\_LOOPED\_流式处理


## <span id="ddk_ksinterface_standard_looped_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_LOOPED_STREAMING_KS"></span>


KSINTERFACE\_标准\_LOOPED\_DSound 的客户端使用流式处理接口。 在 Windows XP 的发布时，Kmixer 和 Portcls 是支持此接口的唯一 KS 音频筛选器。

如果 pin 支持 KSINTERFACE\_标准\_LOOPED\_流式处理相关的筛选器才会完成缓冲区 pin 将被置于*停止*状态。 通过连续循环围绕单个缓冲区中的数据筛选器处理数据提交到筛选器。

### <a name="see-also"></a>另请参阅

[KSINTERFACESETID\_标准](ksinterfacesetid-standard.md)， [ **KSPIN\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff563537)， [ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)

 

 





