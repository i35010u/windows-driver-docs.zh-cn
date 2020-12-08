---
title: 使用默认的 PCL XL 字体
description: 使用默认的 PCL XL 字体
keywords:
- PCL XL 矢量图形 WDK Unidrv，默认字体
- 默认 PCL XL 字体
- 字体 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fa60aa29c6bf36ccb3d5ec560c6a9fa6248b65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835461"
---
# <a name="using-default-pcl-xl-fonts"></a>使用默认的 PCL XL 字体





如果要包含标准 PCL XL 字体，应包含作为 cab 文件的一部分的标准资源 DLL *pclxl.dll*。 以下应出现在 GPD 中的行使用 \* ResourceDLL 特性来指定要使用的资源 DLL。

```cpp
*ResourceDLL: "pclxl.dll"
```

下表列出了 Unidrv 支持的默认 PCL XL 字体：

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
<td><p>ALBERTR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Albertus 特粗"</p></td>
<td><p>ALBERTX.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"老式橄榄色"</p></td>
<td><p>AOLIVEB.UFM</p>
<p>AOLIVEI.UFM</p>
<p>AOLIVER.UFM</p></td>
</tr>
<tr class="even">
<td><p>姚</p></td>
<td><p>ARIALB.UFM</p>
<p>ARIALI.UFM</p>
<p>ARIALJ.UFM</p>
<p>ARIALR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"行楷 Benguiat"</p></td>
<td><p>BENGUATB.UFM</p>
<p>BBENGUATJ.UFM</p>
<p>BENGUATJ.UFM</p>
<p>BENGUATR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"宋体 Bookman"</p></td>
<td><p>BOOKMANB.UFM</p>
<p>BOOKMANJ.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"行楷 Bookman Light"</p></td>
<td><p>BOOKMANI.UFM</p>
<p>BOOKMANR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Brougham"</p></td>
<td><p>BROGHAMB.UFM</p>
<p>BROGHAMI.UFM</p>
<p>BROGHAMJ.UFM</p>
<p>BROGHAMR.UFM</p></td>
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
<td><p>"Clarendon 紧缩"</p></td>
<td><p>CLARCD.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Coronet"</p></td>
<td><p>CORONETR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>宋体</p></td>
<td><p>COURIERB.UFM</p>
<p>COURIERI.UFM</p>
<p>COURIERJ.UFM</p>
<p>COURIERR.UFM</p></td>
</tr>
<tr class="even">
<td><p>宋体</p></td>
<td><p>GARMONDB.UFM</p>
<p>GARMONDI.UFM</p>
<p>GARMONDJ.UFM</p>
<p>GARMONDR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"字母哥特"</p></td>
<td><p>LETGOTHB.UFM</p>
<p>LETGOTHI.UFM</p>
<p>LETGOTHR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Marigold"</p></td>
<td><p>MARGOLDR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"New Roman"</p></td>
<td><p>TIMESNRB.UFM</p>
<p>TIMESNRI.UFM</p>
<p>TIMESNRJ.UFM</p>
<p>TIMESNRR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"Univers 紧缩"</p></td>
<td><p>UNIVERCB.UFM</p>
<p>UNIVERCI.UFM</p>
<p>UNIVERCJ.UFM</p>
<p>UNIVERCR.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Univers"</p></td>
<td><p>通用. UFM</p>
<p>UNIVERSB.UFM</p>
<p>Universc.UFM</p>
<p>Universd.UFM</p>
<p>Universe UFM</p>
<p>UNIVERSI.UFM</p>
<p>UNIVERSJ.UFM</p>
<p>UNIVERSR.UFM</p>
<p>UNIVERSR.UFM</p></td>
</tr>
<tr class="even">
<td><p>"W 丁贝符"</p></td>
<td><p>WDINGBAT.UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Wingdings"</p></td>
<td><p>WINGDING.UFM</p></td>
</tr>
<tr class="even">
<td><p>代号</p></td>
<td><p>代号.UFM</p></td>
</tr>
</tbody>
</table>

 

 

 




