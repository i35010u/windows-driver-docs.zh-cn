---
title: AVC \_ 函数 \_ 获取 \_ EXT \_ 插件 \_ 计数
description: AVC \_ 函数 \_ 获取 \_ EXT \_ 插件 \_ 计数
ms.assetid: dced18ac-dc26-4c47-bc92-a3f3daec505b
keywords:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfaee71a7afc564eefeaf935fb0a2acbebe9a460
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186785"
---
# <a name="avc_function_get_ext_plug_counts"></a>AVC \_ 函数 \_ 获取 \_ EXT \_ 插件 \_ 计数


## <span id="ddk_avc_function_get_ext_plug_counts_ks"></span><span id="DDK_AVC_FUNCTION_GET_EXT_PLUG_COUNTS_KS"></span>


**AVC \_ 函数 \_ 获取 \_ EXT \_ 插件 \_ 计数**函数代码获取外部输入和输出插件计数。

### <a name="io-status-block"></a>I/o 状态块

如果成功，AV/C 协议驱动程序会将 **Irp &gt; IoStatus** 设置为状态 " \_ 成功"。

可能的其他返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出了请求，但在所有超时和重试处理完成之前未收到响应。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>当 IRP 完成状态为 STATUS_REQUEST_ABORTED 时立即中止。 这表明设备已被删除或在1394总线上不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_ *</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>说明

此函数使用 AVC **ExtPlugCounts** \_ MULTIFUNC IRB 结构的 ExtPlugCounts 成员 \_ ，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_EXT_PLUG_COUNTS ExtPlugCounts;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要求

**标头：** 在 *avc*中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 AVC 函数从 AVC 函数枚举 ** \_ \_ 获取 \_ EXT \_ 插件 \_ 计数** \_ 。

<span id="ExtPlugCounts"></span><span id="extplugcounts"></span><span id="EXTPLUGCOUNTS"></span>**ExtPlugCounts**  
指定外部输入和输出插头的计数。

*avc.sys*的虚拟实例不支持此函数代码。

子单位驱动程序负责确定外部插头的函数、格式和使用情况。 但*Avc.sys*会报告外部插头和子单位插头之间的任何永久连接作为子单位上的专用 pin (有关详细信息，请参阅[**AVC \_ FUNCTION \_ GET \_ CONNECTINFO**](avc-function-get-connectinfo.md)) 。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ EXT \_ 插头 \_ 计数**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_ext_plug_counts)， [**AVC \_ 函数**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

