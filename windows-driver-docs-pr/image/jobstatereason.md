---
title: JobStateReason 元素
description: 可选 JobStateReason 元素指定一个作业处于其当前状态的原因。
ms.assetid: daaa288b-fa56-4d29-92f6-0283fbbd2fe8
keywords:
- JobStateReason 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab2809441e4a488a115205a63a56c6f0c92b070a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348778"
---
# <a name="jobstatereason-element"></a>JobStateReason 元素


可选**JobStateReason**元素指定一个作业处于其当前状态的原因。

<a name="usage"></a>用法
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
<td><p>在作业中的图像的数据传输失败。 如果发生此错误，WSD 扫描服务必须中止作业。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCanceledAtDevice"></span><span id="jobcanceledatdevice"></span><span id="JOBCANCELEDATDEVICE"></span>JobCanceledAtDevice</p></td>
<td><p>当前扫描作业已取消在扫描设备的前面板。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobCompletedWithErrors"></span><span id="jobcompletedwitherrors"></span><span id="JOBCOMPLETEDWITHERRORS"></span>JobCompletedWithErrors</p></td>
<td><p>作业已完成，但至少一个错误。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobCompletedWithWarnings"></span><span id="jobcompletedwithwarnings"></span><span id="JOBCOMPLETEDWITHWARNINGS"></span>JobCompletedWithWarnings</p></td>
<td><p>作业已完成，但至少一个警告。 该作业的数据应已成功传输。 此警告可能表示 WSD 扫描服务所做更改到要处理作业的扫描票证。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobScanning"></span><span id="jobscanning"></span><span id="JOBSCANNING"></span>JobScanning</p></td>
<td><p>扫描程序正在将该作业的数据。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobScanningAndTransferring"></span><span id="jobscanningandtransferring"></span><span id="JOBSCANNINGANDTRANSFERRING"></span>JobScanningAndTransferring</p></td>
<td><p>扫描程序正在将该作业的数据，以及数据传输到客户端。</p></td>
</tr>
<tr class="odd">
<td><p><span id="JobTimedOut"></span><span id="jobtimedout"></span><span id="JOBTIMEDOUT"></span>JobTimedOut</p></td>
<td><p>在没有 RetrieveImageRequest 操作及时 CreateScanJobRequest 操作后，WSD 扫描服务已结束该作业。</p></td>
</tr>
<tr class="even">
<td><p><span id="JobTransferring"></span><span id="jobtransferring"></span><span id="JOBTRANSFERRING"></span>JobTransferring</p></td>
<td><p>正在将该作业的数据传输到客户端。</p></td>
</tr>
<tr class="odd">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>无</p></td>
<td><p>作业有任何其他作业的状态信息。</p></td>
</tr>
<tr class="even">
<td><p><span id="ScannerStopped"></span><span id="scannerstopped"></span><span id="SCANNERSTOPPED"></span>ScannerStopped</p></td>
<td><p>扫描设备停止由于存在活动的条件，该作业无法继续，直到条件得到解决。</p></td>
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
<td><p><a href="jobcompletedstatereasons.md" data-raw-source="[&lt;strong&gt;JobCompletedStateReasons&lt;/strong&gt;](jobcompletedstatereasons.md)"><strong>JobCompletedStateReasons</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatereasons.md" data-raw-source="[&lt;strong&gt;JobStateReasons&lt;/strong&gt;](jobstatereasons.md)"><strong>JobStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

必须支持代表可以检测 WSD 扫描服务实现的条件的值。 因此，如果特定支持允许的值的一个子集**JobStateReason**原因是无法检测到在实现中。

您可以扩展允许的值，但扩展此列表对客户端有影响。 客户端通常本地化**JobStateReason**到用户的语言值 （与其他字符串变量的值）。 但是，客户端将无法识别的供应商扩展的值。 客户端可以显示的值，它是接收到"按原样"，但此值将以英文显示，因此某些用户可能无法理解的值。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**JobCompletedStateReasons**](jobcompletedstatereasons.md)

[**JobStateReasons**](jobstatereasons.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






