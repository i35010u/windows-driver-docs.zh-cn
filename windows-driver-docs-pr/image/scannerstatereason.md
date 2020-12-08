---
title: ScannerStateReason 元素
description: 可选的 ScannerStateReason 元素指定有关扫描仪处于其当前状态的原因的一条信息。
keywords:
- ScannerStateReason 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eac7f2bf5d747dafa24ba9ef22a068d9f130ae7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785185"
---
# <a name="scannerstatereason-element"></a>ScannerStateReason 元素


可选的 **ScannerStateReason** 元素指定有关扫描仪处于其当前状态的原因的一条信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerStateReason>
  text
</wscn:ScannerStateReason>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="AttentionRequired"></span><span id="attentionrequired"></span><span id="ATTENTIONREQUIRED"></span>AttentionRequired</p></td>
<td><p>扫描设备需要用户干预，然后才能继续。</p></td>
</tr>
<tr class="even">
<td><p><span id="Calibrating"></span><span id="calibrating"></span><span id="CALIBRATING"></span>校准</p></td>
<td><p>扫描设备正在校准其内部组件，以便准备获取映像。</p></td>
</tr>
<tr class="odd">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>扫描设备中的一个或多个内容已打开。</p></td>
</tr>
<tr class="even">
<td><p><span id="InterlockOpen"></span><span id="interlockopen"></span><span id="INTERLOCKOPEN"></span>InterlockOpen</p></td>
<td><p>互锁处于打开状态。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InternalStorageFull"></span><span id="internalstoragefull"></span><span id="INTERNALSTORAGEFULL"></span>InternalStorageFull</p></td>
<td><p>当前写入的内部存储组件已满。</p></td>
</tr>
<tr class="even">
<td><p><span id="LampError"></span><span id="lamperror"></span><span id="LAMPERROR"></span>LampError</p></td>
<td><p>扫描仪灯出现故障，无法继续进行图像采集。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LampWarming"></span><span id="lampwarming"></span><span id="LAMPWARMING"></span>LampWarming</p></td>
<td><p>扫描仪灯正在预热，准备获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="MediaJam"></span><span id="mediajam"></span><span id="MEDIAJAM"></span>MediaJam</p></td>
<td><p>媒体在一个输入源中卡住，因此图像采集失败。</p></td>
</tr>
<tr class="odd">
<td><p><span id="MultipleFeedError"></span><span id="multiplefeederror"></span><span id="MULTIPLEFEEDERROR"></span>MultipleFeedError</p></td>
<td><p>ADF 同时送入了多片介质。</p></td>
</tr>
<tr class="even">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>内容</p></td>
<td><p>没有当前的状态原因。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Paused"></span><span id="paused"></span><span id="PAUSED"></span>悬停</p></td>
<td><p>扫描仪已暂停，扫描程序状态为 "已停止"。 在此状态下，扫描程序不会生成扫描的输出。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有任何子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerstatereasons.md" data-raw-source="[&lt;strong&gt;ScannerStateReasons&lt;/strong&gt;](scannerstatereasons.md)"><strong>ScannerStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

其中一些原因描述了扫描程序无法根据当前定义的 WSD 扫描服务操作设置输入的扫描程序状态。 例如，即使不存在 "*PauseScanner*" 操作，也可以 **暂停** 扫描仪。 存在这种状态的原因是其他一些协议或控制台操作可能导致扫描程序进入该状态。

WSD 扫描服务必须支持代表其实现中检测到的条件的值。 因此，WSD 扫描服务只能支持它可以检测到的允许值的子集。

您可以扩展允许的值，但在客户端上扩展此列表时可能会有影响。 通常情况下，客户端会将 [**ScannerStateReasons**](scannerstatereasons.md) 值本地化 (与最终用户的语言) 的其他字符串变量值相同，因此客户端将无法识别供应商扩展值。 但是，客户端可以显示直接接收的值。 此值应为英语，因此某些最终用户可能无法理解该值。 或者，扫描服务可以使用一般的 **AttentionRequired** 值，然后在 scanner 控制台上解释问题，用户会在扫描程序中看到该问题。

## <a name="see-also"></a>请参阅


[**ScannerStateReasons**](scannerstatereasons.md)

 

 






