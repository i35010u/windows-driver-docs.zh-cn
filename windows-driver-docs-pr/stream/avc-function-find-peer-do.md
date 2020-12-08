---
title: AVC \_ 函数 \_ 查找 \_ 对等方 \_
description: AVC \_ 函数 \_ 查找 \_ 对等方 \_
keywords:
- AVC_FUNCTION_FIND_PEER_DO 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_FIND_PEER_DO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1a126fcc8a6661892b1dd8b082e8f8c3694ee1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786675"
---
# <a name="avc_function_find_peer_do"></a>AVC \_ 函数 \_ 查找 \_ 对等方 \_


## <span id="ddk_avc_function_find_peer_do_ks"></span><span id="DDK_AVC_FUNCTION_FIND_PEER_DO_KS"></span>


**AVC \_ 函数 \_ FIND \_ 对等 \_ DO** 函数代码查找非虚拟的 *avc.sys* 实例。

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
<td><p>STATUS_UNSUCCESSFUL</p></td>
<td><p>找不到 <em>avc.sys</em> 的非虚拟实例</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INVALID_GENERATION</p></td>
<td><p>在找不到设备对象引用之前发生了总线重置。 获取新 NodeAddress，然后重试。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>注释

此函数使用 AVC **PeerLocator** \_ MULTIFUNC IRB 结构的 PeerLocator 成员 \_ ，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PEER_DO_LOCATOR PeerLocator;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要求

**标头：** 在 *avc* 中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 **AVC \_ 函数 \_ 查找 \_ 对 \_ 等** AVC \_ 函数枚举。

<span id="PeerLocator"></span><span id="peerlocator"></span><span id="PEERLOCATOR"></span>**PeerLocator**  
指定 *avc.sys* 的非虚拟 (对等) 实例。

此函数根据其表示的设备的节点地址，查找非虚拟的 *avc.sys* 实例。 如果找不到实例，则 IRP 完成，状态状态为 "不 \_ 成功"。 定位实例后，调用方可以通过对象提交任何 GUID \_ AVC \_ 类设备接口请求。 调用方必须释放对此对象的引用， (通过 **ObDereferenceObject**) 完成此操作。

可以在 IRQL &lt; = 调度级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**AVC \_ 对等方 \_ DO \_ 定位器**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_peer_do_locator)、 [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

