---
title: AVC\_函数\_获取\_子单位\_信息
description: AVC\_函数\_获取\_子单位\_信息
ms.assetid: 1793df9d-b186-425f-a3dd-3054cb9b74bf
keywords:
- AVC_FUNCTION_GET_SUBUNIT_INFO 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_SUBUNIT_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aba7def57219a1e799dafdda71b4cfd1181deca5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845080"
---
# <a name="avc_function_get_subunit_info"></a>AVC\_函数\_获取\_子单位\_信息


## <span id="ddk_avc_function_get_subunit_info_ks"></span><span id="DDK_AVC_FUNCTION_GET_SUBUNIT_INFO_KS"></span>


**AVC\_函数\_获取\_子单位\_INFO**函数代码获取目标设备的子单位信息。

### <a name="io-status-block"></a>I/O 状态块

此函数始终将**Irp&gt;IoStatus**的状态设置\_为 "成功"。

### <a name="comments"></a>备注

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**子单元连接**成员，如下所示。

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

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  
必须将此成员的**函数**submember 设置为**AVC\_函数，\_** 从 AVC\_函数枚举获取\_子组\_信息。

<span id="Subunits"></span><span id="subunits"></span><span id="SUBUNITS"></span>**子单元连接**  
指定 AV/C 子单位的信息的说明。

此函数在本地完成，因此不会将任何命令发送到目标。

此函数代码可在 IRQL &lt;= 调度\_级别调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_子区域\_INFO\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_subunit_info_block)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





