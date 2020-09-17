---
title: 强制的目标与连接的目标
description: 强制的目标与连接的目标
ms.assetid: 690e585b-3c90-4373-844d-42afe033b59b
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、强制与连接的目标
- 正在连接显示 WDK Windows Server 2008 R2 显示、CCD 的概念、强制与连接的目标
- 配置显示 WDK Windows 7 显示、CCD 概念、强制与连接的目标
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、强制与连接的目标
- CCD 概念 WDK Windows 7 显示、强制与连接的目标
- CCD 概念 WDK Windows Server 2008 R2 显示、强制与连接的目标
- 强制的与连接的目标 WDK Windows 7 显示
- 强制的与连接的目标 WDK Windows Server 2008 R2 显示
- 连接与强制目标 WDK Windows 7 显示
- 连接与强制目标 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9795ed25f4471bf64d8164b3eb7a6dad05ee3b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717228"
---
# <a name="forced-versus-connected-targets"></a>强制的目标与连接的目标


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

CCD Api 介绍连接的监视器和 forceable 目标的概念。 如果 GPU 能够检测到监视器的状态（这是监视器和目标的物理属性），则监视器将连接到该目标。 如果 GPU 即使 GPU 无法检测到连接的监视器也能将显示信号发送出目标，则目标为 forceable。 所有模拟目标类型都被视为 forceable，并且所有数字目标都不被视为 forceable。 下表描述了在路径处于活动状态且不处于活动状态时已连接状态和强制状态的组合。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径-活动状态</th>
<th align="left">路径强制状态</th>
<th align="left">监视器-连接状态</th>
<th align="left">结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>可用</p></td>
<td align="left"><p>Forced</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>由于监视器已连接并且处于活动状态，因此已启用目标输出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可用</p></td>
<td align="left"><p>Forced</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>启用目标输出，因为路径是强制的，并且处于活动状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可用</p></td>
<td align="left"><p>未强制</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>由于监视器已连接并且处于活动状态，因此已启用目标输出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可用</p></td>
<td align="left"><p>未强制</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>无法设置路径，因为它不是强制的，并且未连接监视器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不活动</p></td>
<td align="left"><p>Forced</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>可以启用目标输出，因为它是强制的，并且已连接监视器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>不活动</p></td>
<td align="left"><p>Forced</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>目标输出可以启用，因为它是强制的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不活动</p></td>
<td align="left"><p>未强制</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>可以启用目标输出，因为已连接监视器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>不活动</p></td>
<td align="left"><p>未强制</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>无法启用目标输出，因为未连接监视器，并且路径不是强制的。</p></td>
</tr>
</tbody>
</table>

 

下表描述了每个路径的几种可能的强制状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">强制状态</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>正常强制</p></td>
<td align="left"><p>当电源转换、重新启动或强制状态关闭后，此强制状态将丢失。</p></td>
</tr>
<tr class="even">
<td align="left"><p>路径-持久</p></td>
<td align="left"><p>重新启动后，此强制状态将丢失。 即使路径中的监视器是<strong>ChangeDisplaySettingsEx</strong>调用的目标，Microsoft Win32 <strong>ChangeDisplaySettingsEx</strong>函数也始终销毁所有路径保存的监视器。 如果调用方使用<em>Flags</em>参数中设置的 SDC_USE_SUPPLIED_DISPLAY_CONFIG 或 SDC_TOPOLOGY_SUPPLIED 标志来调用<a href="/windows/win32/api/winuser/nf-winuser-setdisplayconfig" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](/windows/win32/api/winuser/nf-winuser-setdisplayconfig)"><strong>SetDisplayConfig</strong></a> CCD 函数，则如果新拓扑不包括监视器所在的路径，则<strong>SetDisplayConfig</strong>将删除路径保存的监视器。 对于调用方在 <em>flags</em> 参数中指定的所有其他 SDC_TOPOLOGY_XXX 标志，除非调用方还指定了 SDC_PATH_PERSIST_IF_REQUIRED 标志，并且路径在新拓扑中处于活动状态，否则， <strong>SetDisplayConfig</strong> 将删除路径持久监视器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>引导持久</p></td>
<td align="left"><p>此强制状态仅在关闭时丢失。 此状态在系统重启之间保持不变。</p></td>
</tr>
</tbody>
</table>

 

