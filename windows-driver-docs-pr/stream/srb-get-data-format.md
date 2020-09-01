---
title: SRB \_ 获取 \_ 数据 \_ 格式
description: SRB \_ 获取 \_ 数据 \_ 格式
ms.assetid: 6346d719-395d-4847-af80-6c65e15af250
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b037250a1c63a9b6bf735900007d88729042e578
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186093"
---
# <a name="srb_get_data_format"></a>SRB \_ 获取 \_ 数据 \_ 格式


## <span id="ddk_srb_get_data_format_ks"></span><span id="DDK_SRB_GET_DATA_FORMAT_KS"></span>


类驱动程序发出此请求以查询流的数据格式。 微型驱动程序应将*pSrb* - &gt; **CommandData**设置为流的当前数据格式。

有关数据格式的详细信息，请参阅 [Stream 类微型驱动程序 Design Guide](./streaming-minidrivers2.md)。

 

