---
title: Serenum 的注册表设置
description: Serenum 的注册表设置
ms.assetid: c8a8f1b7-ea58-49ed-98e0-40297ec9a769
keywords:
- Serenum 驱动程序 WDK、 注册表设置
- 注册表 WDK 串行设备
- 串行设备 WDK、 注册表设置
- 串行设备 WDK，Serenum 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128249a1ec0591190b4c2763a05edda3f8663484
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522140"
---
# <a name="registry-settings-for-serenum"></a>Serenum 的注册表设置





本主题介绍 Serenum 使用 RS-232 端口在 Microsoft Windows 2000 及更高版本的项值。

下面的注册表条目值是 RS-232 端口插硬件设备注册表项下：

<a href="" id="portname--reg-sz-"></a>**PortName** (REG\_SZ)  
指定的端口的名称。 Serenum 读取此值，并在响应中返回的端口名称[ **IOCTL\_SERENUM\_获取\_端口\_名称**](https://msdn.microsoft.com/library/windows/hardware/ff546533)请求。

<a href="" id="identifier--reg-sz-"></a>**标识符**(REG\_SZ)  
指定的端口的名称。 Serenum 读取此值。 为支持**标识符**条目值仅为与某些旧的 PCMCIA 设备兼容性而提供。 利用**标识符**条目值已过时，不应与在 Windows 2000 和更高版本的驱动程序实现。 Serenum 返回端口名称，以响应 IOCTL\_SERENUM\_获取\_端口\_名称请求。

<a href="" id="skipenumerations--reg-dword-"></a>**SkipEnumerations** (REG\_DWORD)  
在 Windows XP 及更高版本，此项值控制当 Serenum 枚举响应中的端口[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)征求**BusRelations**。 Windows 2000 不支持此项值。

每次系统将生成一个串行端口设备堆栈时，设置 Serenum*枚举模式*它使用枚举一个端口。 端口的设备堆栈，Serenum 的初始化过程[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程中读取的端口**SkipEnumerations**条目值，并将作为枚举模式设置下表中所述。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>枚举模式</th>
<th>SkipEnumerations 值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>通常情况下枚举。</p></td>
<td><p>0x00000000</p>
<p>（或值项不存在）</p></td>
<td><p>Serenum 枚举所有响应中的串行端口<strong>BusRelations</strong>请求 （无论是通过系统启动或用户通过设备管理器或添加硬件向导启动）。</p></td>
</tr>
<tr class="even">
<td><p>跳过指定的数目的枚举。</p></td>
<td><p>到 0xFFFFFFE 0x00000001 之间的值</p></td>
<td><p>Serenum 跳过指定的枚举数，并随后在通常情况下枚举，只要端口保持启用状态。</p></td>
</tr>
<tr class="odd">
<td><p>跳过所有枚举。</p></td>
<td><p>0xFFFFFFFF</p></td>
<td><p>Serenum 永远不会枚举一个端口。 必须手动安装连接到该端口的设备。</p></td>
</tr>
</tbody>
</table>

 

例如，如果一个串行端口**SkipEnumerations**项值设置为 3 时系统将生成端口设备堆栈，Serenum 将跳过前三个**BusRelations**它为端口收到的请求。 只要端口保持启用状态，Serenum 随后将以正常方式枚举该端口。

 

 




