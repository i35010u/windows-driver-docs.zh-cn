---
title: AVC \_ 函数 \_ 获取 \_ 唯一 \_ ID
description: AVC \_ 函数 \_ 获取 \_ 唯一 \_ ID
keywords:
- AVC_FUNCTION_GET_UNIQUE_ID 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_UNIQUE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93fe53564df365a2cf6c1ade9a75c1c6ae3810ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830897"
---
# <a name="avc_function_get_unique_id"></a>AVC \_ 函数 \_ 获取 \_ 唯一 \_ ID


## <span id="ddk_avc_function_get_unique_id_ks"></span><span id="DDK_AVC_FUNCTION_GET_UNIQUE_ID_KS"></span>


**AVC \_ 函数 \_ 获取 \_ 唯一 \_ id** 函数代码获取 AV/C 单元的唯一 id。

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
<th>描述</th>
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

 

### <a name="comments"></a>注释

此函数使用 AVC **UniqueID** \_ MULTIFUNC IRB 结构的 UniqueID 成员 \_ ，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_UNIQUE_ID UniqueID;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

AVC \_ 唯一 ID 结构的成员如下 \_ 所示：

```cpp
typedef struct _AVC_UNIQUE_ID {
    OUT GUID DeviceID;
} AVC_UNIQUE_ID, *PAVC_UNIQUE_ID;
```

### <a name="requirements"></a>要求

**标头：** 在 *avc* 中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
必须将此成员的 **函数** submember 设置为 AVC 函数 GET AVC 函数枚举中的 **\_ \_ \_ 唯一 \_ ID** \_ 。

<span id="UniqueID"></span><span id="uniqueid"></span><span id="UNIQUEID"></span>**UniqueID**  
指定一个 GUID，它表示整个单元。 同一单元内的所有子单元连接共享同一 GUID。 不能有两个单位共享同一 GUID。

*avc.sys* 的虚拟实例不支持此函数代码。

如果子单元驱动程序必须将设备 GUID 报告给某个应用程序，而该应用程序必须知道多个子单位驱动程序实例中的哪个 (属于同一单元) ，或者它为外部插头构建其自己的 AVCPRECONNECTINFO 结构，则它将使用此函数。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ UNIQUE \_ ID**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_unique_id)， [**AVCPRECONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)， [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

