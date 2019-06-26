---
title: AVC\_FUNCTION\_GET\_UNIQUE\_ID
description: AVC\_FUNCTION\_GET\_UNIQUE\_ID
ms.assetid: 51b35686-03a9-45b3-8bdc-14cbd24714dc
keywords:
- AVC_FUNCTION_GET_UNIQUE_ID 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_UNIQUE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c691d3d7cbfc9972e3c7c565f1c2ebcd952a8d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386727"
---
# <a name="avcfunctiongetuniqueid"></a>AVC\_FUNCTION\_GET\_UNIQUE\_ID


## <span id="ddk_avc_function_get_unique_id_ks"></span><span id="DDK_AVC_FUNCTION_GET_UNIQUE_ID_KS"></span>


**AVC\_函数\_获取\_UNIQUE\_ID**函数代码获取 AV/C 单元的唯一 ID。

### <a name="io-status-block"></a>I/O 状态块

如果成功，AV/C 协议驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功。

可能其他返回值包括：

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
<td><p>发出请求，但未收到响应之前所有的超时和重试处理已完成。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>立即中止 STATUS_REQUEST_ABORTED IRP 完成状态时。 这表示设备已删除或不再可用的 1394年总线上。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示错误或警告发生了超出范围的 AV/C 协议。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用**UniqueID**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

成员的 AVC\_UNIQUE\_ID 结构如下所示：

```cpp
typedef struct _AVC_UNIQUE_ID {
    OUT GUID DeviceID;
} AVC_UNIQUE_ID, *PAVC_UNIQUE_ID;
```

### <a name="requirements"></a>要求

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_UNIQUE\_ID**从 AVC\_函数枚举。

<span id="UniqueID"></span><span id="uniqueid"></span><span id="UNIQUEID"></span>**UniqueID**  
指定一个 GUID，表示作为一个整体的单位。 在相同单元中的所有子单元连接共享相同的 GUID。 没有两个单位共享相同的 GUID。

个虚拟实例不支持此函数代码*avc.sys*。

子单元驱动程序使用此函数，如果必须向控制应用程序 （必须知道哪个许多子单元的驱动程序实例的应用程序属于相同单元中），将错误报告设备 GUID 或者如果它构建自己 AVCPRECONNECTINFO 结构外部插入。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)， [ **AVC\_UNIQUE\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_unique_id)， [ **AVCPRECONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcpreconnectinfo)， [ **AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





