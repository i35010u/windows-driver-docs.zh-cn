---
title: Windows 8 中的 Direct3D 软件要求
description: 本主题介绍支持 Microsoft Direct3D Windows 8 中的软件要求。
ms.assetid: EB9AB15A-4E47-48AE-AE39-6051F8FC39A8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50ad434b8d769ba7189b442ff67b1e06fd7b0d05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391217"
---
# <a name="direct3d-software-requirements-in-windows-8"></a>Windows 8 中的 Direct3D 软件要求


本主题介绍支持 Microsoft Direct3D Windows 8 中的软件要求。

对于 Windows 8，独立硬件供应商必须编写可以支持相关的 Direct3D 功能级别的用户模式驱动程序的 Windows 显示器驱动程序模型 (WDDM) 1.2 驱动程序 (UMD) 设备驱动程序接口 (DDIs)。

例如，Microsoft Direct3D 9 支持的硬件必须，最小值，支持 Direct3D 版本 9 DDI。 这些要求各不相同的软件根据此表中指定的 Microsoft DirectX 硬件级别：

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
<td align="left"><p>必需：WDDM 1.2</p>
<p>必需：D3D9 - UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D10</td>
<td align="left"><p>必需：WDDM 1.2</p>
<p>必需：D3D9 - UMD DDI</p>
<p>必需：D3D10 UMD DDI</p>
<p>必需：D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D10.1</td>
<td align="left"><p>必需：WDDM 1.2</p>
<p>必需：D3D9 - UMD DDI</p>
<p>必需：D3D10 UMD DDI</p>
<p>必需：D3D10.1 UMD DDI</p>
<p>必需：D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="even">
<td align="left">D3D11</td>
<td align="left"><p>必需：WDDM 1.2</p>
<p>必需：D3D9 - UMD DDI</p>
<p>必需：D3D10 UMD DDI</p>
<p>必需：D3D10.1 UMD DDI</p>
<p>必需：D3D11 - UMD DDI</p>
<p>必需：D3D11.1 - UMD DDI</p></td>
</tr>
<tr class="odd">
<td align="left">D3D11.1</td>
<td align="left"><p>必需：WDDM 1.2</p>
<p>必需：D3D9 - UMD DDI</p>
<p>必需：D3D10 UMD DDI</p>
<p>必需：D3D10.1 UMD DDI</p>
<p>必需：D3D11 - UMD DDI</p>
<p>必需：D3D11.1 - UMD DDI</p></td>
</tr>
</tbody>
</table>

 

下表描述了在 Windows 8 中使用用户模式驱动程序 (UMD) DDI 更改公开的功能。

**D3D9-UMD DDI 公开 Windows 8 中的以下新功能**

| 是否为必需？ | 功能                  |
|-----------|--------------------------|
| 必需  | 不覆盖并丢弃 |
| 必需  | Tileable 复制标志       |

 

**D3D11.1-UMD DDI 公开 Windows 8 中的各功能级别 10，10.1、 11 和 11.1 了以下新功能**

| 是否为必需？      | 功能                                                                            |
|----------------|------------------------------------------------------------------------------------|
| 必需       | 不覆盖并丢弃                                                           |
| 必需       | 支持跨进程共享的纹理数组 （包括立体 3D）    |
| 必需       | Tileable 复制标志                                                                 |
| 必需       | ClearView                                                                          |
| 如果实现 | 逻辑操作                                                                          |
| 必需       | 像素格式 (5551，565、 4444)-完全支持跨功能级别而异        |
| 必需       | 同一个面 blits                                                                 |
| 必需       | 部分常量缓冲区更新                                                    |
| 必需       | 偏移量常量缓冲区绑定                                                        |
| 必需       | 改进的资源共享                                                          |
| 必需       | SampleCount = 1 （有限独立于目标的光栅化 (TIR) 上 10 和 10.1，11） |

 

**D3D11.1-UMD DDI 公开的以下新功能的功能级别 11 和 11.1**

| 是否为必需？      | 功能                                   |
|----------------|-------------------------------------------|
| 必需       | UAV-MSAA                                  |
| 如果实现 | 双精度着色器功能     |
| 必需       | (MSAD) 的绝对差异的掩码的总和 |

 

**D3D11.1-UMD DDI 公开的以下新功能的功能级别 11.1**

| 是否为必需？ | 功能                  |
|-----------|--------------------------|
| 必需  | 在每个阶段的 Uav      |
| 必需  | UAV MSAA （在 16 示例） |
| 必需  | TIR                      |

 

 

 





