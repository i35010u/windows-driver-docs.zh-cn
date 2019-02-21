---
title: SRB\_获取\_数据\_格式
description: SRB\_获取\_数据\_格式
ms.assetid: 6346d719-395d-4847-af80-6c65e15af250
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf6a952c1560b170f622e57299e4b005816152f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543615"
---
# <a name="srbgetdataformat"></a>SRB\_获取\_数据\_格式


## <span id="ddk_srb_get_data_format_ks"></span><span id="DDK_SRB_GET_DATA_FORMAT_KS"></span>


在类驱动程序发出此请求，以查询该流的数据格式。 微型驱动程序应设置*pSrb*-&gt;**CommandData**到流的当前数据格式。

有关数据格式的详细信息，请参阅[Stream 类微型驱动程序设计指南](https://msdn.microsoft.com/library/windows/hardware/ff568277)。

 

 





