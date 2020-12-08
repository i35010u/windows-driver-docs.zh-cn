---
title: Windows 8 中的 Direct3D 软件要求
description: 本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的软件要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 357ad02066e6a9ca582210ff2b5ddb8ca208d293
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826051"
---
# <a name="direct3d-software-requirements-in-windows-8"></a>Windows 8 中的 Direct3D 软件要求


本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的软件要求。

对于 Windows 8，独立硬件供应商必须编写一个 Windows 显示驱动程序模型 (WDDM) 1.2 驱动程序，该驱动程序可以支持 (UMD) 设备驱动程序接口 (DDIs) 的相关 Direct3D 功能级别用户模式驱动程序。

例如，Microsoft Direct3D 9 的硬件至少必须支持 Direct3D 版本 9 DDI。 根据此表中指定的 Microsoft DirectX 硬件级别，这些软件要求会有所不同：

**DirectX 软件要求**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectX 硬件</th>
<th align="left">软件要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">D3D9</td>
<td align="left"><p>必需： WDDM 1。2</p>
<p>必需： D3D9-UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D10</td>
<td align="left"><p>必需： WDDM 1。2</p>
<p>必需： D3D9-UMD DDI</p>
<p>必需： D3D10-UMD DDI</p>
<p>必需： D3D 11.1-UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D 10。1</td>
<td align="left"><p>必需： WDDM 1。2</p>
<p>必需： D3D9-UMD DDI</p>
<p>必需： D3D10-UMD DDI</p>
<p>必需： D3D 10.1-UMD DDI</p>
<p>必需： D3D 11.1-UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D11</td>
<td align="left"><p>必需： WDDM 1。2</p>
<p>必需： D3D9-UMD DDI</p>
<p>必需： D3D10-UMD DDI</p>
<p>必需： D3D 10.1-UMD DDI</p>
<p>必需： D3D11-UMD DDI</p>
<p>必需： D3D 11.1-UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D 11。1</td>
<td align="left"><p>必需： WDDM 1。2</p>
<p>必需： D3D9-UMD DDI</p>
<p>必需： D3D10-UMD DDI</p>
<p>必需： D3D 10.1-UMD DDI</p>
<p>必需： D3D11-UMD DDI</p>
<p>必需： D3D 11.1-UMD DDI</p></td>
</tr>
</tbody>
</table>

 

下表描述了在 Windows 8 中使用用户模式驱动程序 (UMD) DDI 更改公开的功能。

**D3D9-UMD DDI 公开 Windows 8 中的以下新功能**

| 必需？ | 功能                  |
|-----------|--------------------------|
| 必须  | 无覆盖和丢弃 |
| 必须  | Tileable 复制标志       |

 

**D3D 11.1-UMD DDI 在功能级别10、10.1、11和11.1 范围内公开 Windows 8 中的以下新功能**

| 必需？      | 功能                                                                            |
|----------------|------------------------------------------------------------------------------------|
| 必须       | 无覆盖和丢弃                                                           |
| 必须       | 支持跨进程共享纹理数组 (包括 Stereoscopic 3D)     |
| 必须       | Tileable 复制标志                                                                 |
| 必须       | ClearView                                                                          |
| 如果实现 | 逻辑操作数                                                                          |
| 必须       | 像素格式 (5551、565、4444) 完全支持因功能级别而异        |
| 必须       | 相同 surface blits                                                                 |
| 必须       | 部分常量缓冲区更新                                                    |
| 必须       | 偏移常数缓冲区绑定                                                        |
| 必须       | 改进的资源共享                                                          |
| 必须       | SampleCount = 1 (限制与目标无关的光栅化 (TIR) 10、10.1 和 11)  |

 

**D3D 11.1-UMD DDI 公开了以下功能级别 11 & 11.1 的新功能**

| 必需？      | 功能                                   |
|----------------|-------------------------------------------|
| 必须       | UAV-MSAA                                  |
| 如果实现 | 双精度着色器功能     |
| 必须       | MSAD) 的绝对差异的掩码总和 ( |

 

**D3D 11.1-UMD DDI 公开功能级别11.1 的下列新功能**

| 必需？ | 功能                  |
|-----------|--------------------------|
| 必须  | 每个阶段的 Uav      |
| 必须  | UAV- (16 个样本)  |
| 必须  | TIR                      |

 

 

 





