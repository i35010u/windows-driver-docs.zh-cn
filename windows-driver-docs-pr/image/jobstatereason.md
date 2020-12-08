---
title: JobStateReason 元素
description: 可选的 JobStateReason 元素指定作业处于其当前状态的原因之一。
keywords:
- JobStateReason 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 401e445e30ebb10455794b56f2847c391a92b8e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805587"
---
# <a name="jobstatereason-element"></a>JobStateReason 元素


可选的 **JobStateReason** 元素指定作业处于其当前状态的原因之一。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobStateReason>
  text
</wscn:JobStateReason>
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
<td><p><span id="InvalidScanTicket"></span><span id="invalidscanticket"></span><span id="INVALIDSCANTICKET"></span>InvalidScanTicket</p></td>
<td><p>作业被拒绝，因为 WSD 扫描服务无法处理 ScanTicket。</p></td>
</tr>
<tr class="even">
<td><p><span id="DocumentFormatError"></span><span id="documentformaterror"></span><span id="DOCUMENTFORMATERROR"></span>DocumentFormatError</p></td>
<td><p>WSD 扫描服务不支持请求的文档格式。</p></td>
</tr>
<tr class="odd">
<td><p><span id="ImageTransferError"></span><span id="imagetransfererror"></span><span id="IMAGETRANSFERERROR"></span>ImageTransferError</p></td>
<td><p>作业中映像的数据传输失败。 如果发生此错误，则 WSD 扫描服务必须中止该作业。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCanceledAtDevice"></span><span id="jobcanceledatdevice"></span><span id="JOBCANCELEDATDEVICE"></span>JobCanceledAtDevice</p></td>
<td><p>在扫描设备的前面板上取消了当前扫描作业。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobCompletedWithErrors"></span><span id="jobcompletedwitherrors"></span><span id="JOBCOMPLETEDWITHERRORS"></span>JobCompletedWithErrors</p></td>
<td><p>作业已完成，但至少有一个错误。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCompletedWithWarnings"></span><span id="jobcompletedwithwarnings"></span><span id="JOBCOMPLETEDWITHWARNINGS"></span>JobCompletedWithWarnings</p></td>
<td><p>作业已完成，但至少出现一个警告。 应成功传输作业数据。 此警告可能表明 WSD 扫描服务已更改扫描票证来处理作业。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobScanning"></span><span id="jobscanning"></span><span id="JOBSCANNING"></span>JobScanning</p></td>
<td><p>扫描仪将作业数据数字化。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobScanningAndTransferring"></span><span id="jobscanningandtransferring"></span><span id="JOBSCANNINGANDTRANSFERRING"></span>JobScanningAndTransferring</p></td>
<td><p>扫描仪将作业数据数字化，并将数据传输到客户端。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobTimedOut"></span><span id="jobtimedout"></span><span id="JOBTIMEDOUT"></span>JobTimedOut</p></td>
<td><p>在 RetrieveImageRequest 操作后，WSD 扫描服务将结束该作业，并及时执行 CreateScanJobRequest 操作。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobTransferring"></span><span id="jobtransferring"></span><span id="JOBTRANSFERRING"></span>JobTransferring</p></td>
<td><p>正在将作业数据传输到客户端。</p></td>
</tr>
<tr class="odd">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>内容</p></td>
<td><p>该作业没有与作业状态有关的其他信息。</p></td>
</tr>
<tr class="even">
<td><p><span id="ScannerStopped"></span><span id="scannerstopped"></span><span id="SCANNERSTOPPED"></span>ScannerStopped</p></td>
<td><p>扫描设备因活动状态而停止，作业无法继续，直到解决该问题。</p></td>
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
<td><p><a href="jobcompletedstatereasons.md" data-raw-source="[&lt;strong&gt;JobCompletedStateReasons&lt;/strong&gt;](jobcompletedstatereasons.md)"><strong>JobCompletedStateReasons</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatereasons.md" data-raw-source="[&lt;strong&gt;JobStateReasons&lt;/strong&gt;](jobstatereasons.md)"><strong>JobStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

必须支持表示 WSD 扫描服务实现可以检测的条件的值。 因此，如果在实现中无法检测到特定的 **JobStateReason** 原因，则只能支持一个允许值的子集。

您可以扩展允许的值，但扩展此列表会影响客户端。 通常情况下，客户端将 **JobStateReason** 值本地化 (与其他) 到用户语言的字符串变量值相同。 但是，客户端将无法识别供应商扩展的值。 客户端可以显示 "按原样" 接收的值，但此值将以英文显示，因此某些用户可能无法理解该值。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**JobCompletedStateReasons**](jobcompletedstatereasons.md)

[**JobStateReasons**](jobstatereasons.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






