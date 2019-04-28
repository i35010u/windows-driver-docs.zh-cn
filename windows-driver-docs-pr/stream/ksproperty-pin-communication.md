---
title: KSPROPERTY\_PIN\_通信
description: KSPROPERTY\_PIN\_通信属性指定 IRP 流的方向上通过 pin 工厂实例化的 pin。
ms.assetid: d5f62731-39de-4ec4-83d5-f4253373aaa4
keywords:
- KSPROPERTY_PIN_COMMUNICATION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_COMMUNICATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb32eaffe880d7ae06b2e3990ae1dc2ece2c6fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346457"
---
# <a name="kspropertypincommunication"></a>KSPROPERTY\_PIN\_通信


KSPROPERTY\_PIN\_通信属性指定 IRP 流的方向上通过 pin 工厂实例化的 pin。

## <span id="ddk_ksproperty_pin_communication_ks"></span><span id="DDK_KSPROPERTY_PIN_COMMUNICATION_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_COMMUNICATION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 筛选器返回了以下值，该值指定此 pin 工厂实例化一个 pin 的通信方向之一：

<span id="KSPIN_COMMUNICATION_NONE"></span><span id="kspin_communication_none"></span>KSPIN\_通信\_NONE  
Pin 工厂不会实例化任何 pin。

<span id="KSPIN_COMMUNICATION_SINK"></span><span id="kspin_communication_sink"></span>KSPIN\_通信\_接收器  
Pin 工厂实例化 IRP 接收器 pin。 此类 pin 只能连接到 IRP 源 pin。

<span id="KSPIN_COMMUNICATION_SOURCE"></span><span id="kspin_communication_source"></span>KSPIN\_通信\_源  
Pin 工厂实例化 IRP 源 pin。 此类 pin 只能连接到 IRP 接收器 pin。

<span id="KSPIN_COMMUNICATION_BOTH"></span><span id="kspin_communication_both"></span>KSPIN\_通信\_两者  
Pin 工厂实例化是 IRP 接收器和 IRP 源的 pin。

<span id="KSPIN_COMMUNICATION_BRIDGE"></span><span id="kspin_communication_bridge"></span>KSPIN\_通信\_桥  
此 pin 不能连接到其他 pin，但不能在其能够接收非 KS I/O 请求创建实例。

源 pin 发送 Irp 到接收器的 pin。 源 pin 可读取或写入数据，以及接收器 pin 可能包含到其读取或写入从它的数据。 有关详细信息，请参阅[ **KSPROPERTY\_PIN\_数据流**](ksproperty-pin-dataflow.md)。

Stream 微型驱动程序不需要直接; 处理此属性stream 类驱动程序处理使用 Stream 请求块到查询的详细信息，在必要时此属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_PIN\_DATAFLOW**](ksproperty-pin-dataflow.md)

 

 






