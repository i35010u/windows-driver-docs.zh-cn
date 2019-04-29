---
title: WHEA 策略设置
description: WHEA 策略设置
ms.assetid: 65ef70b7-a517-4428-9e6d-09c6da84e798
keywords:
- 预计故障分析 (PFA) WDK WHEA，注册表设置
- WDK WHEA 的注册表设置
- 注册表设置 WDK WHEA，预计故障分析 (PFA)
- 策略设置 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbafed57b2ffb0e88de467d680cab4006e7b6c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384735"
---
# <a name="whea-policy-settings"></a>WHEA 策略设置


预测故障分析 (PFA) 执行的 Windows 硬件错误体系结构 (WHEA)，是通过使用注册表设置配置。 WHEA 计算机系统启动时读取这些注册表设置。 对这些设置进行任何更改需要重新启动系统，以使其生效。

从 Windows 8 开始，WHEA 策略可以是托管类型但[ **WHEAPolicyManagementMethods** ](https://msdn.microsoft.com/library/windows/hardware/hh451252)或通过 WHEA Powershell 模块。 如果通过任一这些模式进行了更新策略，策略值将立即生效。

**请注意**  本主题中所述的注册表设置适用于使用 WHEA 通过仅。 如果[特定于平台的硬件错误驱动程序 (PSHED) 插件](platform-specific-hardware-error-driver-plug-ins2.md)执行 PFA，并使用注册表来存储其配置设置，它必须使用不同于本主题中描述的注册表值。

 

WHEA PFA 配置设置位于以下注册表项：

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\WHEA\Policy
```

**请注意**  WHEA 假定 PFA 注册表值的默认设置，如果该值不存在下**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\WHEA\\策略**。

 

下表介绍用于 PFA 配置各种注册表值。 下表中的注册表值是 REG\_DWORD 值。

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
<td><p>一个布尔值，该值指定 WHEA 是否可通过使用 PFA 执行脱机的硬件组件。 WHEA 使硬件组件，例如 ECC 内存页脱机时 PFA （WHEA 或 PSHED 插件由执行） 确定模块已超出错误阈值。</p>
<div class="alert">
<strong>请注意</strong>   <strong>DisableOffline</strong>值将应用到预测由于 WHEA 或 PSHED 插件 PFA 执行而失败的硬件组件。
</div>
<div>
 
</div>
<p>值为 0 将启用硬件脱机支持。 任何其他值禁用硬件脱机支持。</p>
<p>此设置的默认值为 0。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPersistOffline</strong></p></td>
<td><p>一个布尔值，指定是否 WHEA 使其脱机的 ECC 内存页保持不变中引导配置数据 (BCD) 存储。 如果在 BCD 存储中保持不变，ECC 内存页后将采取脱机立即重新启动系统。</p>
<div class="alert">
<strong>请注意</strong>   <strong>MemPersistOffline</strong>值适用于脱机由于 WHEA 或 PSHED 插件 PFA 执行 ECC 内存页。
</div>
<div>
 
</div>
<p>如果值为 1 表示启用 BCD 持续性。 值为 0 会禁用 BCD 持久性。</p>
<p>为此设置默认值为 1 的 Windows Server 平台，使用 0 表示 Windows 客户端平台。</p></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaDisable</strong></p></td>
<td><p>一个布尔值，该值指定是否禁用 WHEA 的 PFA ECC 内存页。</p>
<p>值为 0 启用 PFA ECC 内存页。 任何其他值禁用 PFA ECC 内存页。</p>
<p>此设置的默认值为 0。</p></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaPageCount</strong></p></td>
<td><p>一个值，指定最大 WHEA 监视 PFA ECC 内存页面数。</p>
<p>此值可介于 1 和 65536 之间。 默认值为 64。</p>
<div class="alert">
<strong>请注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td><p></p>
<p><strong>MemPfaThreshold</strong></p></td>
<td><p>一个值，指定最大错误数 ECC 内存页上允许 WHEA 正在监视。</p>
<p>当错误数超过此阈值时，WHEA 停止监视内存页，并尝试使内存页处于脱机状态。</p>
<p>此值可介于 1 和 65536 之间。 默认值为 16。</p>
<div class="alert">
<strong>请注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p></p>
<p><strong>MemPfaTimeout</strong></p></td>
<td><p>指定 ECC 内存页的时间长度值，单位为秒，由 WHEA for PFA 监视。</p>
<p>WHEA 开始监视 ECC 内存页的第一个错误检测到内存页时。</p>
<p>WHEA 停止监视 ECC 内存页时出现以下项之一：</p>
<ul>
<li><p>监视间隔已超出<strong>MemPfaTimeout</strong>值。</p></li>
<li><p>检测到的错误数已超出<strong>MemPfaThreshold</strong>值。</p></li>
</ul>
<p>此值可介于 0 和 604800 （7 天） 之间。 零值指定的被监视的内存页将永远不会超时。默认值为 86400 （24 小时）。</p>
<div class="alert">
<strong>请注意</strong>  如果此值设置为允许范围之外的数字，则使用默认值。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

应用程序兼容性原因支持以下两个旧注册表值：

<a href="" id="singlebiteccerrorthreshold"></a>**SingleBitEccErrorThreshold**  
此值对应于**MemPfaThreshold**注册表值。

<a href="" id="maxcorrectedmceoutstanding"></a>**MaxCorrectedMCEOutstanding**  
此值对应于**MemPfaPageCount**注册表值。

**请注意**  只要可能，应使用而不是这些旧的注册表值本主题中前面所述的注册表值。

 

 

 




