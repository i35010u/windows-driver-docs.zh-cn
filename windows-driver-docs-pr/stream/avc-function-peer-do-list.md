---
title: AVC \_ 函数 \_ 对等 \_ DO \_ LIST
description: AVC \_ 函数 \_ 对等 \_ DO \_ LIST
ms.assetid: 80ffd94e-788f-4874-b716-3eb66d90e4aa
keywords:
- AVC_FUNCTION_PEER_DO_LIST 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_PEER_DO_LIST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f4e33c3762a64b174ea9a878f884843497ab6b2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187491"
---
# <a name="avc_function_peer_do_list"></a>AVC \_ 函数 \_ 对等 \_ DO \_ LIST


## <span id="ddk_avc_function_peer_do_list_ks"></span><span id="DDK_AVC_FUNCTION_PEER_DO_LIST_KS"></span>


**AVC \_ 函数 \_ 对等 \_ DO \_ LIST**函数代码查找所有非*avc.sys*虚拟的实例。

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
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>无法获取设备对象引用列表的空间。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>说明

此函数使用 AVC **PeerList** \_ MULTIFUNC IRB 结构的 PeerList 成员 \_ ，如下所示。

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

**标头：** 在 *avc*中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 **AVC \_ 函数对等 AVC 函数枚举中的 \_ \_ DO \_ LIST** \_ 。

<span id="PeerList"></span><span id="peerlist"></span><span id="PEERLIST"></span>**PeerList**  
指定 *avc.sys*的所有非虚拟 (对等) 实例的列表。

调用方可以 \_ \_ 通过对象列表中返回的任何对象提交 GUID AVC 类设备接口请求。 调用方必须释放对这些对象的引用 (通过 **ObDereferenceObject**) ，并在完成时通过 **ExFreePool**) 释放包含列表 (的内存。

可以在 IRQL &lt; = 调度级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**AVC \_ 等 \_ DO \_ LIST**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_peer_do_list)、 [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**DEVICE \_ OBJECT**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)、 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)、 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)

 

