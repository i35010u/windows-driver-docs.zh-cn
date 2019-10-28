---
title: KSINTERFACE\_标准\_循环\_流式处理
description: KSINTERFACE\_标准\_循环\_流式处理
ms.assetid: c12e7085-fa13-48d3-b4ed-ea0a708f026b
keywords:
- KSINTERFACE_STANDARD_LOOPED_STREAMING 流媒体设备
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_LOOPED_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925deb2d8f0ca73d6389e3bf051517eeefa8f846
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838868"
---
# <a name="ksinterface_standard_looped_streaming"></a>KSINTERFACE\_标准\_循环\_流式处理


## <span id="ddk_ksinterface_standard_looped_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_LOOPED_STREAMING_KS"></span>


DSound 的客户端使用 KSINTERFACE\_标准\_循环\_流式处理接口。 在 Windows XP 发布时，Kmixer 和 Portcls 是唯一支持此接口的 KS 音频筛选器。

如果 pin 支持 KSINTERFACE\_标准\_循环\_流式处理，则相关筛选器将不会完成缓冲区，直到将 pin 置于*停止*状态。 筛选器通过连续循环遍历提交给筛选器的单个缓冲区中的数据来处理数据。

### <a name="see-also"></a>另请参阅

[KSINTERFACESETID\_Standard](ksinterfacesetid-standard.md)、 [**KSPIN\_INTERFACE**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))、 [**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)

 

 





