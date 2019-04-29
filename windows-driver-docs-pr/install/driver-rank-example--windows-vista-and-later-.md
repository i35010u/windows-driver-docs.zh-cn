---
title: 驱动程序分级示例
description: 驱动程序分级示例
ms.assetid: 20fe0f63-5d6c-4617-b5df-b2adb941f257
keywords:
- 驱动程序级别范围 WDK 设备安装
- 排名范围 WDK 设备安装
- 范围排名 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c87ab0ba7bd37ab336afc6eca445a44aea595a28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356017"
---
# <a name="driver-rank-example"></a>驱动程序分级示例


请考虑具有以下的列表的设备[设备标识字符串](device-identification-strings.md)，其中 HwID_*N*和 CID_*N*名称表示实际[硬件Id](hardware-ids.md)并[兼容 Id](compatible-ids.md):

-   硬件 Id 列表
    ```cpp
     HwID_1, HwID_2
    ```

-   兼容 Id 列表
    ```cpp
    CID_1, and CID_2
    ```

中 Id 列表的第一个硬件 ID 是硬件的设备的最特定标识符。 在此示例中，这是 HwID_1。

此外假定存在一个具有的 INF 文件[ **INF*模型*部分**](inf-models-section.md)具有以下条目，其中 INF_*XXX_N*名称表示实际的硬件 Id 和兼容 Id:

```cpp
DeviceDesc1 = InstallSection1, INF_HWID_1, INF_CID_1, INF_CID_2
```

此外，假定 INF *DDInstall*名为部分*InstallSection1*具有以下**FeatureScore**指令，其中的相应功能的分数驱动程序是 0x00*GG*0000:

```cpp
FeatureScore=0xGG
```

下表列出了由设备报告的标识符和 INF 中列出的标识符之间每个可能的匹配项的排名*模型*部分项。 排名是总和[签名分数](signature-score--windows-vista-and-later-.md)，这将表现 0x*SS*000000，[功能分数](feature-score--windows-vista-and-later-.md)，由数据 0x00 表示*GG*0000，并[标识符分数](identifier-score--windows-vista-and-later-.md)，这取决于每种情况下，在两个匹配的标识符。

<table>
<tr>
<th>设备标识符</th>
<th colspan="3">INF 中的标识符<i>模型</i>节条目</th>
</tr>
<tr>
<td></td>
<td>
<p><b>INF_HwID_1</b></p>
</td>
<td>
<p><b>INF_CID_1</b></p>
</td>
<td>
<p><b>INF_CID_2</b></p>
</td>
</tr>
<tr>
<td>
<p><b>HwID_1</b></p>
</td>
<td>
<p>排名 0x<i>SSGG</i>0000</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>1000年</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>1000年</p>
</td>
</tr>
<tr>
<td>
<p><b>HwID_2</b></p>
</td>
<td>
<p>排名 0x<i>SSGG</i>0001</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>1001年</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>1001年</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_1</b></p>
</td>
<td>
<p>排名 0x<i>SSGG</i>2000年</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>3000</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>3100</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_2</b></p>
</td>
<td>
<p>排名 0x<i>SSGG</i>2001年</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>3001</p>
</td>
<td>
<p>排名 0x<i>SSGG</i>3101</p>
</td>
</tr>
</table>

 


