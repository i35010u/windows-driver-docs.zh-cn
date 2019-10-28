---
title: KSINTERFACE\_标准\_流式处理
description: KSINTERFACE\_标准\_流式处理
ms.assetid: 04ba6879-1699-4d12-b81e-a90878014325
keywords:
- KSINTERFACE_STANDARD_STREAMING 流媒体设备
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e29062db17a3675cbf5bd03b4adc073136b7f73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838866"
---
# <a name="ksinterface_standard_streaming"></a>KSINTERFACE\_标准\_流式处理


## <span id="ddk_ksinterface_standard_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_STREAMING_KS"></span>


KSINTERFACE\_标准\_流接口在大多数 KS 音频筛选器之间使用，并受所有音频微型端口支持。 如果 pin 支持此接口，则相关筛选器将处理每个[ **\_KSSTREAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)中嵌入的数据一次。

### <a name="see-also"></a>另请参阅

[KSINTERFACESETID\_Standard](ksinterfacesetid-standard.md)、 [**KSPIN\_INTERFACE**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))、 [**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)、 [**KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)

 

 





