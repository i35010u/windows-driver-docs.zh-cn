---
title: SRB\_设置\_数据\_格式
description: SRB\_设置\_数据\_格式
ms.assetid: a111ab92-a0a0-464e-ac13-f5be33ecd064
keywords:
- SRB_SET_DATA_FORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_SET_DATA_FORMAT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75b6d550981ce1d1717984ebb3ded4ed6fe2a57a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525879"
---
# <a name="srbsetdataformat"></a>SRB\_设置\_数据\_格式


## <span id="ddk_srb_set_data_format_ks"></span><span id="DDK_SRB_SET_DATA_FORMAT_KS"></span>


在类驱动程序发出此请求，以流的数据格式设置。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_SUPPORTED"></span><span id="status_not_supported"></span>状态\_不\_支持  
指示微型驱动程序不支持请求的数据格式。

### <a name="comments"></a>备注

在类驱动程序将传递中的新数据格式**CommandData**。**OpenFormat**的成员*pSrb*指针。 (此指针指向[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构。)

有关数据格式的详细信息，请参阅[Stream 类微型驱动程序设计指南](https://msdn.microsoft.com/library/windows/hardware/ff568277)。 另请参阅[AVStream 中的数据范围交集](https://msdn.microsoft.com/library/windows/hardware/ff558680)。

 

 





