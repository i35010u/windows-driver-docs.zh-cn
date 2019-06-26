---
title: AVC\_FUNCTION\_GET\_SUBUNIT\_INFO
description: AVC\_FUNCTION\_GET\_SUBUNIT\_INFO
ms.assetid: 1793df9d-b186-425f-a3dd-3054cb9b74bf
keywords:
- AVC_FUNCTION_GET_SUBUNIT_INFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_SUBUNIT_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6fb39823daa65d533720a2e85d9c266b7d32c4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386736"
---
# <a name="avcfunctiongetsubunitinfo"></a>AVC\_FUNCTION\_GET\_SUBUNIT\_INFO


## <span id="ddk_avc_function_get_subunit_info_ks"></span><span id="DDK_AVC_FUNCTION_GET_SUBUNIT_INFO_KS"></span>


**AVC\_函数\_获取\_子单元\_信息**函数代码中获得目标设备的子单元信息。

### <a name="io-status-block"></a>I/O 状态块

此函数始终设置**Irp-&gt;IoStatus.Status**于状态\_成功。

### <a name="comments"></a>备注

此函数使用**子单元连接**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_SUBUNIT_INFO_BLOCK Subunits;
 };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要求

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_子单元\_信息**从 AVC\_函数枚举。

<span id="Subunits"></span><span id="subunits"></span><span id="SUBUNITS"></span>**子单元连接**  
指定 AV/C 子单元的信息的说明。

因此没有命令发送到目标本地，满足此函数。

可能在 IRQL 调用此函数代码&lt;= 调度\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)， [ **AVC\_子单元\_信息\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_subunit_info_block)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





