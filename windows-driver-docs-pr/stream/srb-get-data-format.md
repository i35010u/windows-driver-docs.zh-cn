---
title: SRB\_获取\_数据\_格式
description: SRB\_获取\_数据\_格式
ms.assetid: 6346d719-395d-4847-af80-6c65e15af250
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97ca335c49fe880799ce8f94ef4eb2841a5a9358
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358379"
---
# <a name="srbgetdataformat"></a>SRB\_获取\_数据\_格式


## <span id="ddk_srb_get_data_format_ks"></span><span id="DDK_SRB_GET_DATA_FORMAT_KS"></span>


在类驱动程序发出此请求，以查询该流的数据格式。 微型驱动程序应设置*pSrb*-&gt;**CommandData**到流的当前数据格式。

有关数据格式的详细信息，请参阅[Stream 类微型驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)。

 

 





