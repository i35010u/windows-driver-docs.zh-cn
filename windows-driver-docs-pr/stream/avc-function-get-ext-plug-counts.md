---
title: AVC\_函数\_获取\_EXT\_插入\_计数
description: AVC\_函数\_获取\_EXT\_插入\_计数
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
ms.openlocfilehash: e633c45f67e6ea7af0dfbef327a94e15e63f3bff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844658"
---
# <a name="avc_function_get_ext_plug_counts"></a>AVC\_函数\_获取\_EXT\_插入\_计数


## <span id="ddk_avc_function_get_ext_plug_counts_ks"></span><span id="DDK_AVC_FUNCTION_GET_EXT_PLUG_COUNTS_KS"></span>


**AVC\_函数\_GET\_EXT\_即插\_计数**函数代码获取外部输入和输出插件计数。

### <a name="io-status-block"></a>I/O 状态块

如果成功，AV/C 协议驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

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
<td><p>当 IRP 完成状态为 "STATUS_REQUEST_ABORTED" 时立即中止。 这表明设备已被删除或在1394总线上不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**ExtPlugCounts**成员，如下所示。

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

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  
此成员的**函数**submember 必须设置为 AVC\_函数\_从 AVC\_函数枚举**获取\_EXT\_插入\_计数**。

<span id="ExtPlugCounts"></span><span id="extplugcounts"></span><span id="EXTPLUGCOUNTS"></span>**ExtPlugCounts**  
指定外部输入和输出插头的计数。

*Avc*的虚拟实例不支持此函数代码。

子单位驱动程序负责确定外部插头的函数、格式和使用情况。 不过， *Avc*将外部插头和子单位插头之间的任何永久连接报告为子单位的专用 pin （有关详细信息，请参阅[**Avc\_函数\_GET\_CONNECTINFO**](avc-function-get-connectinfo.md)）。

此名称必须以 IRQL = 被动\_级别进行调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_EXT\_插入\_计数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_ext_plug_counts)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





