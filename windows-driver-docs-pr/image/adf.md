---
title: ADF 元素
description: 可选 ADF 元素描述附加到扫描仪 (ADF) 自动文档送纸器的功能。
keywords:
- ADF 元素图像处理设备
topic_type:
- apiref
api_name:
- wscn ADF
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc22f4be18dc3513a8ec1144b58bbac730a95b6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837771"
---
# <a name="adf-element"></a>ADF 元素


可选 **ADF** 元素描述附加到扫描仪 (ADF) 自动文档送纸器的功能。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADF>
  child elements
</wscn:ADF>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfsupportsduplex.md" data-raw-source="[&lt;strong&gt;ADFSupportsDuplex&lt;/strong&gt;](adfsupportsduplex.md)"><strong>ADFSupportsDuplex</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备有 ADF，则 WSD 扫描服务必须提供所有 **ADF** 子元素的配置信息。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ADFSupportsDuplex**](adfsupportsduplex.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






