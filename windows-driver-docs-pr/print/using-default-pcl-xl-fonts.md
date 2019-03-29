---
title: 使用默认的 PCL XL 字体
description: 使用默认的 PCL XL 字体
ms.assetid: 8e6abae5-c86f-4cfc-a379-2dd3f8810474
keywords:
- PCL XL 矢量图形 WDK Unidrv，默认字体
- 默认 PCL XL 字体
- 字体 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db9235d061d8a655c194563bfba89ec2d209c21
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464283"
---
# <a name="using-default-pcl-xl-fonts"></a>使用默认的 PCL XL 字体





如果你想要包括的标准的 PCL XL 字体，则应包含标准的资源 DLL， *pclxl.dll*，作为该 cab 文件的一部分。 以下行，应显示在 GPD，使用\*项 ResourceDLL 属性来指定要使用的 DLL 的资源。

```cpp
*ResourceDLL: "pclxl.dll"
```

Unidrv 支持默认 PCL XL 字体下表中列出了：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>字体名称</th>
<th>字体文件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"Albertus Medium"</p></td>
<td><p>ALBERTR。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Albertus 额外加粗"</p></td>
<td><p>ALBERTX.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"古董橄榄色"</p></td>
<td><p>AOLIVEB.UFM</p>
<p>AOLIVEI.UFM</p>
<p>AOLIVER。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Arial"</p></td>
<td><p>ARIALB。UFM</p>
<p>ARIALI。UFM</p>
<p>ARIALJ.UFM</p>
<p>ARIALR。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"黑 Benguiat"</p></td>
<td><p>BENGUATB。UFM</p>
<p>BBENGUATJ.UFM</p>
<p>BENGUATJ.UFM</p>
<p>BENGUATR。UFM</p></td>
</tr>
<tr class="even">
<td><p>"黑 Bookman 细"</p></td>
<td><p>BOOKMANB.UFM</p>
<p>BOOKMANJ.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"黑 Bookman Light"</p></td>
<td><p>BOOKMANI。UFM</p>
<p>BOOKMANR。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Brougham"</p></td>
<td><p>BROGHAMB。UFM</p>
<p>BROGHAMI。UFM</p>
<p>BROGHAMJ.UFM</p>
<p>BROGHAMR。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"CG Omega"</p></td>
<td><p>CGOMEGAB.UFM</p>
<p>CGOMEGAI.UFM</p>
<p>CGOMEGAJ.UFM</p>
<p>CGOMEGAR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"CG 时间"</p></td>
<td><p>CGTIMESB.UFM</p>
<p>CGTIMESI.UFM</p>
<p>CGTIMESJ.UFM</p>
<p>CGTIMESR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Clarendon 压缩"</p></td>
<td><p>CLARCD.UFM</p></td>
</tr>
<tr class="even">
<td><p>"公司"</p></td>
<td><p>CORONETR。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Courier"</p></td>
<td><p>COURIERB.UFM</p>
<p>COURIERI.UFM</p>
<p>COURIERJ.UFM</p>
<p>COURIERR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Garamond"</p></td>
<td><p>GARMONDB。UFM</p>
<p>GARMONDI.UFM</p>
<p>GARMONDJ.UFM</p>
<p>GARMONDR。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"字母文"</p></td>
<td><p>LETGOTHB。UFM</p>
<p>LETGOTHI.UFM</p>
<p>LETGOTHR。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Marigold"</p></td>
<td><p>MARGOLDR。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"宋体"</p></td>
<td><p>TIMESNRB.UFM</p>
<p>TIMESNRI.UFM</p>
<p>TIMESNRJ.UFM</p>
<p>TIMESNRR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"压缩 Univers"</p></td>
<td><p>UNIVERCB.UFM</p>
<p>UNIVERCI.UFM</p>
<p>UNIVERCJ.UFM</p>
<p>UNIVERCR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Univers"</p></td>
<td><p>Universa.UFM</p>
<p>UNIVERSB.UFM</p>
<p>Universc.UFM</p>
<p>Universd.UFM</p>
<p>Universe.UFM</p>
<p>UNIVERSI.UFM</p>
<p>UNIVERSJ.UFM</p>
<p>UNIVERSR.UFM</p>
<p>UNIVERSR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"W 丁贝符"</p></td>
<td><p>WDINGBAT。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Wingdings"</p></td>
<td><p>WINGDING.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Symbol"</p></td>
<td><p>SYMBOL.UFM</p></td>
</tr>
</tbody>
</table>

 

 

 




