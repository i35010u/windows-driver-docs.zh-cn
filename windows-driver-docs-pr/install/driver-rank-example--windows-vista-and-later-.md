---
title: 驱动程序分级示例
description: 驱动程序分级示例
keywords:
- 驱动程序排名范围 WDK 设备安装
- 排名范围 WDK 设备安装
- 范围排名 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d2d85a8363116c91de1b9e55b597e265a68b250
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782721"
---
# <a name="driver-rank-example"></a>驱动程序分级示例


请考虑一个设备，其中包含以下 [设备标识字符串](device-identification-strings.md)列表，其中 HwID_ *n* 和 CID_ *N* 名称表示实际的 [硬件 id](hardware-ids.md) 和 [兼容 id](compatible-ids.md)：

-   硬件 Id 列表
    ```cpp
     HwID_1, HwID_2
    ```

-   兼容 Id 列表
    ```cpp
    CID_1, and CID_2
    ```

硬件 Id 列表中的第一个硬件 ID 是设备的最特定标识符。 在此示例中，HwID_1。

还假设存在 [**一个 inf *Models* 文件**](inf-models-section.md)，其中包含以下条目，其中的 INF_ *XXX_N* 名称表示实际的硬件 id 和兼容 id：

```cpp
DeviceDesc1 = InstallSection1, INF_HWID_1, INF_CID_1, INF_CID_2
```

此外，假定名为 *InstallSection1* 的 INF *DDInstall* 部分具有以下 **FeatureScore** 指令，其中，驱动程序的相应功能分数为 0x00 *GG* 0000：

```cpp
FeatureScore=0xGG
```

下表列出了设备报告的标识符与 "INF *模型* " 部分条目中列出的标识符之间的每个可能匹配的排名。 排名是 [签名分数](signature-score--windows-vista-and-later-.md)的总和，该分数由 0x *SS* 000000 表示， [功能分数](feature-score--windows-vista-and-later-.md)由 0x00 *GG* 0000 表示，而 [标识符分数](identifier-score--windows-vista-and-later-.md)在每种情况下，它取决于两个匹配的标识符。

<table>
<tr>
<th>设备标识符</th>
<th colspan="3">INF <i>模型</i> 部分条目中的标识符</th>
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
<p>Rank 0x<i>SSGG</i>0000</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>1000</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>1000</p>
</td>
</tr>
<tr>
<td>
<p><b>HwID_2</b></p>
</td>
<td>
<p>级别 0x<i>SSGG</i>0001</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>1001</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>1001</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_1</b></p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>2000</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>3000</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>3100</p>
</td>
</tr>
<tr>
<td>
<p><b>CID_2</b></p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>2001</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>3001</p>
</td>
<td>
<p>Rank 0x<i>SSGG</i>3101</p>
</td>
</tr>
</table>

 


