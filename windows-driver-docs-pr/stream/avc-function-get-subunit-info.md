---
title: AVC \_ 函数 \_ 获取子单位 \_ \_ 信息
description: AVC \_ 函数 \_ 获取子单位 \_ \_ 信息
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
ms.openlocfilehash: f1d50d98ac94274df602ad610cf2a52428dc92b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816511"
---
# <a name="avc_function_get_subunit_info"></a>AVC \_ 函数 \_ 获取子单位 \_ \_ 信息


## <span id="ddk_avc_function_get_subunit_info_ks"></span><span id="DDK_AVC_FUNCTION_GET_SUBUNIT_INFO_KS"></span>


**AVC 函数获取子单位 \_ \_ \_ \_ 信息** 函数代码获取目标设备的子单位信息。

### <a name="io-status-block"></a>I/o 状态块

此函数始终将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"。

### <a name="comments"></a>注释

此函数使用 AVC **Subunits** \_ MULTIFUNC IRB 结构的子单元连接成员 \_ ，如下所示。

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

**标头：** 在 *avc* 中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 AVC 函数从 AVC 函数枚举 **获取子 \_ 工作 \_ \_ \_ 信息** \_ 。

<span id="Subunits"></span><span id="subunits"></span><span id="SUBUNITS"></span>**子单元连接**  
指定 AV/C 子单位的信息的说明。

此函数在本地完成，因此不会将任何命令发送到目标。

可以在 IRQL &lt; = 调度级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC 子单位 \_ \_ INFO \_ BLOCK**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_subunit_info_block)， [**AVC \_ 函数**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

