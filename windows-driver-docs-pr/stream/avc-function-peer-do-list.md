---
title: AVC\_函数\_对等方\_执行\_列表
description: AVC\_函数\_对等方\_执行\_列表
ms.assetid: 80ffd94e-788f-4874-b716-3eb66d90e4aa
keywords:
- AVC_FUNCTION_PEER_DO_LIST 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_PEER_DO_LIST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcf8bff68757c53652db812fa93de5641e977be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386725"
---
# <a name="avcfunctionpeerdolist"></a>AVC\_函数\_对等方\_执行\_列表


## <span id="ddk_avc_function_peer_do_list_ks"></span><span id="DDK_AVC_FUNCTION_PEER_DO_LIST_KS"></span>


**AVC\_函数\_对等方\_不要\_列表**函数代码查找所有非虚拟*avc.sys*实例。

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
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>无法获取有关列表的设备对象引用的空间。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用**PeerList**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PEER_DO_LIST PeerList;
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
**函数**必须设置为此成员的子**AVC\_函数\_对等方\_执行\_列表**从 AVC\_函数枚举。

<span id="PeerList"></span><span id="peerlist"></span><span id="PEERLIST"></span>**PeerList**  
指定的所有非虚拟 （对等） 实例的列表*avc.sys*。

调用方可能会提交 GUID\_AVC\_类设备接口请求的任何对象通过返回对象列表中。 调用方必须释放对这些对象的引用 (通过**ObDereferenceObject**)，并释放内存包含列表 (通过**ExFreePool**) 完成。

可能在 IRQL 调用此函数代码&lt;= 调度\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)， [ **AVC\_对等方\_执行\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_peer_do_list)， [ **AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)， [**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)， [ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)， [ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)

 

 





