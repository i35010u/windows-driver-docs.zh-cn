---
title: ADF 元素
description: 可选的 ADF 元素介绍自动文档送纸器 (ADF) 附加到扫描程序的功能。
ms.assetid: 2c9114c3-0c6e-4404-a1ee-fd8d63c6e8eb
keywords:
- ADF 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADF
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04aac63bfc0dee8260860181214aaf3baedf1e6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542069"
---
# <a name="adf-element"></a>ADF 元素


可选**ADF**元素描述自动文档送纸器 (ADF) 附加到扫描程序的功能。

<a name="usage"></a>用法
-----

```xml
<wscn:ADF>
  child elements
</wscn:ADF>
```

<a name="attributes"></a>属性
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

如果扫描设备具有 ADF，WSD 扫描服务必须提供所有的配置信息**ADF**子元素。

## <a name="see-also"></a>另请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ADFSupportsDuplex**](adfsupportsduplex.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






