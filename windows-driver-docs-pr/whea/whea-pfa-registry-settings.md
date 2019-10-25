---
title: WHEA 策略设置
description: WHEA 策略设置
ms.assetid: 65ef70b7-a517-4428-9e6d-09c6da84e798
keywords:
- 预测性故障分析（PFA） WDK WHEA，注册表设置
- 注册表设置 WDK WHEA
- 注册表设置 WDK WHEA、预测性故障分析（PFA）
- 策略设置 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c01cf7c897b949cf64556de9c6d5650edbbbbc9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828929"
---
# <a name="whea-policy-settings"></a>WHEA 策略设置


通过使用注册表设置来配置 Windows 硬件错误体系结构（WHEA）所执行的预测性故障分析（PFA）。 当计算机系统启动时，WHEA 将读取这些注册表设置。 对这些设置进行的任何更改都需要重新启动系统才能使其生效。

从 Windows 8 开始，可以通过[**WHEAPolicyManagementMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)或通过 WHEA Powershell 模块管理 WHEA 策略。 如果通过上述任一模式更新策略，策略值将立即生效。

**请注意**   本主题中所述的注册表设置仅供 WHEA 使用。 如果[特定于平台的硬件错误驱动程序（PSHED）插件](platform-specific-hardware-error-driver-plug-ins2.md)执行 PFA 并使用注册表存储其配置设置，则它必须使用与本主题中描述的注册表值不同的注册表值。

 

WHEA PFA 配置设置位于以下注册表项中：

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WHEA\Policy
```

**请注意**  如果**HKEY\_本地\_机\\SYSTEM\\CurrentControlSet\\控件中不存在 PFA 注册表值的默认设置，则 WHEA\\\\** .

 

下表描述了用于 PFA 配置的各种注册表值。 下表中的注册表值为 REG\_DWORD 值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表值名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p>
<p><strong>DisableOffline</strong></p></td>
<td><p>一个布尔值，指定 WHEA 是否可以通过使用 PFA 使硬件组件脱机。 WHEA 使用一个硬件组件（如 ECC 内存页），只要 PFA （由 WHEA 或 PSHED 插件执行），就会确定该模块已超过错误阈值。</p>
<div class="alert">
<strong>请注意</strong>  <strong>DisableOffline</strong>值适用于由于 PFA 执行 WHEA 或 PSHED 插件而导致失败的硬件组件。
</div>
<div>
 
</div>
<p>值0实现硬件脱机支持。 任何其他值将禁用硬件脱机支持。</p>
<p>此设置的默认值为0。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPersistOffline</strong></p></td>
<td><p>一个布尔值，指定 WHEA 脱机的 ECC 内存页面是否在引导配置数据（BCD）存储中保留。 如果在 BCD 存储中保持，则在系统重新启动后，ECC 内存页将立即脱机。</p>
<div class="alert">
<strong>请注意</strong>  <strong>MemPersistOffline</strong>值适用于由于 PFA 执行 WHEA 或 PSHED 插件而脱机的 ECC 内存页面。
</div>
<div>
 
</div>
<p>如果值为1，则启用 BCD 持久。 值0将禁用 BCD 暂留。</p>
<p>对于 Windows Server 平台，此设置的默认值为1，对于 Windows 客户端平台，此值为0。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaDisable</strong></p></td>
<td><p>一个布尔值，指定是否禁用用于 ECC 内存页的 WHEA 的 PFA。</p>
<p>如果值为0，则为 ECC 内存页启用 PFA。 任何其他值将禁用 ECC 内存页的 PFA。</p>
<p>此设置的默认值为0。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaPageCount</strong></p></td>
<td><p>一个值，该值指定 WHEA 为 PFA 监视的 ECC 内存页的最大数目。</p>
<p>此值可以介于1到65536之间。 默认值为64。</p>
<div class="alert">
<strong>注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaThreshold</strong></p></td>
<td><p>一个值，该值指定 WHEA 监视的 ECC 内存页上允许的最大错误数。</p>
<p>当错误数超过此阈值时，WHEA 将停止监视内存页并尝试使内存页脱机。</p>
<p>此值可以介于1到65536之间。 默认值为16。</p>
<div class="alert">
<strong>注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaTimeout</strong></p></td>
<td><p>一个以秒为单位的值，该值指定 WHEA for PFA 的 ECC 内存页的监视时长。</p>
<p>当检测到该内存页的第一个错误时，WHEA 开始监视 ECC 内存页。</p>
<p>当发生以下情况之一时，WHEA 停止监视 ECC 内存页：</p>
<ul>
<li><p>监视间隔已超过<strong>MemPfaTimeout</strong>值。</p></li>
<li><p>检测到的错误数已超过<strong>MemPfaThreshold</strong>值。</p></li>
</ul>
<p>此值可以介于0和604800（7天）之间。 如果值为零，则指定监视的内存页将永远不会超时。默认值为86400（24小时）。</p>
<div class="alert">
<strong>注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

以下两个旧注册表值支持应用程序兼容性原因：

<a href="" id="singlebiteccerrorthreshold"></a>**SingleBitEccErrorThreshold**  
此值对应于**MemPfaThreshold**注册表值。

<a href="" id="maxcorrectedmceoutstanding"></a>**MaxCorrectedMCEOutstanding**  
此值对应于**MemPfaPageCount**注册表值。

**请注意**  应尽可能使用本主题前面所述的注册表值，而不是这些旧的注册表值。

 

 

 




