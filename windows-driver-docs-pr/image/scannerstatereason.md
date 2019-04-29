---
title: ScannerStateReason 元素
description: 可选 ScannerStateReason 元素指定一条有关扫描程序处于其当前状态的信息。
ms.assetid: 7f10476a-d3ef-40a1-a355-ab735a6afe60
keywords:
- ScannerStateReason 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5442865363ffa6dc9ab774d8fbf29e1d57a031a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370046"
---
# <a name="scannerstatereason-element"></a>ScannerStateReason 元素


可选**ScannerStateReason**元素指定一条有关扫描程序处于其当前状态的信息。

<a name="usage"></a>用法
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
<td><p>扫描设备校准及其内部组件进行准备，以便获取映像。</p></td>
</tr>
<tr class="odd">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>一个扫描设备上的多个后台处于打开状态。</p></td>
</tr>
<tr class="even">
<td><p><span id="InterlockOpen"></span><span id="interlockopen"></span><span id="INTERLOCKOPEN"></span>InterlockOpen</p></td>
<td><p>互锁处于打开状态。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InternalStorageFull"></span><span id="internalstoragefull"></span><span id="INTERNALSTORAGEFULL"></span>InternalStorageFull</p></td>
<td><p>当前正在写入到的内部存储组件已满。</p></td>
</tr>
<tr class="even">
<td><p><span id="LampError"></span><span id="lamperror"></span><span id="LAMPERROR"></span>LampError</p></td>
<td><p>扫描程序 lamp 失败的原因和图像采集无法继续。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LampWarming"></span><span id="lampwarming"></span><span id="LAMPWARMING"></span>LampWarming</p></td>
<td><p>扫描程序 lamp 正在预热进行准备，以便获取映像。</p></td>
</tr>
<tr class="even">
<td><p><span id="MediaJam"></span><span id="mediajam"></span><span id="MEDIAJAM"></span>MediaJam</p></td>
<td><p>媒体被印象中其中一个输入源，因此图像获取失败。</p></td>
</tr>
<tr class="odd">
<td><p><span id="MultipleFeedError"></span><span id="multiplefeederror"></span><span id="MULTIPLEFEEDERROR"></span>MultipleFeedError</p></td>
<td><p>ADF 是同时提供多个的介质。</p></td>
</tr>
<tr class="even">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>无</p></td>
<td><p>没有当前状态说明。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Paused"></span><span id="paused"></span><span id="PAUSED"></span>已暂停</p></td>
<td><p>扫描程序已暂停，并扫描程序状态为已停止。 在此状态下，扫描程序不会产生扫描生成的输出。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有子元素。

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

其中一些原因描述扫描程序不能根据当前定义的 WSD 扫描服务操作一组输入的扫描程序状态。 例如，可以是扫描程序**已暂停**即使没有任何"*PauseScanner*"操作。 因为某些其他协议或控制台操作可能会导致扫描程序进入该状态，这种状态都存在。

WSD 扫描服务必须支持代表将在其实现可检测的条件的值。 因此，WSD 扫描服务可以支持仅可以检测到的允许值的子集。

您可以扩展允许的值，但扩展此列表在客户端上的时会有影响。 客户端通常本地化[ **ScannerStateReasons** ](scannerstatereasons.md)值 （与其他字符串变量的值） 为最终用户的语言，因此客户端将无法识别供应商扩展值。 但是，客户端可以显示直接接收的值。 此值应在英语中，因此一些最终用户可能无法理解的值。 此外，扫描服务可以使用常规**AttentionRequired**值，然后在扫描程序控制台中，用户将看到当它们是在扫描仪上说明问题。

## <a name="see-also"></a>请参阅


[**ScannerStateReasons**](scannerstatereasons.md)

 

 






