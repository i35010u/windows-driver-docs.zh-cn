---
title: AVC\_函数\_获取\_EXT\_即插即用\_计数
description: AVC\_函数\_获取\_EXT\_即插即用\_计数
ms.assetid: dced18ac-dc26-4c47-bc92-a3f3daec505b
keywords:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1066f6f3e212febce7745c86dbf1197f46035a92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331703"
---
# <a name="avcfunctiongetextplugcounts"></a>AVC\_函数\_获取\_EXT\_即插即用\_计数


## <span id="ddk_avc_function_get_ext_plug_counts_ks"></span><span id="DDK_AVC_FUNCTION_GET_EXT_PLUG_COUNTS_KS"></span>


**AVC\_函数\_获取\_EXT\_插入\_计数**函数代码获取外部输入和输出插入计数。

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

此函数使用**ExtPlugCounts**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_EXT\_即插即用\_计数**从 AVC\_函数的枚举。

<span id="ExtPlugCounts"></span><span id="extplugcounts"></span><span id="EXTPLUGCOUNTS"></span>**ExtPlugCounts**  
指定的外部输入和输出插入的计数。

个虚拟实例不支持此函数代码*avc.sys*。

子单元驱动程序负责确定函数、 格式和外部插入的使用。 *Avc.sys*的确会但是，报告任何外部插入和子单元插入之间的永久连接专用图钉形式子单元 (有关详细信息，请参阅[ **AVC\_函数\_GET\_CONNECTINFO**](avc-function-get-connectinfo.md))。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)， [ **AVC\_EXT\_即插即用\_计数**](https://msdn.microsoft.com/library/windows/hardware/ff554143)， [**AVC\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

 

 





