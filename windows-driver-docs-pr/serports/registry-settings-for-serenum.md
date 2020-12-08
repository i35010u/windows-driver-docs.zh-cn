---
title: 用于 Serenum 的注册表设置
description: 用于 Serenum 的注册表设置
keywords:
- Serenum 驱动程序 WDK，注册表设置
- 注册表 WDK 串行设备
- 串行设备 WDK，注册表设置
- 串行设备 WDK，Serenum 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a5448bc628a37be585447d72867b2d926b7a7de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804991"
---
# <a name="registry-settings-for-serenum"></a>用于 Serenum 的注册表设置

本主题介绍 Serenum 在 Microsoft Windows 2000 和更高版本中用于 RS-232 端口的条目值。

以下注册表项值位于 RS-232 端口的 "即插即用硬件设备" 注册表项下：

<a href="" id="portname--reg-sz-"></a>**Portvalue** (REG \_ SZ)   
指定端口的名称。 Serenum 读取此值，并返回端口名称以响应 [**IOCTL \_ Serenum \_ 获取 \_ 端口 \_ 名称**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serenum_get_port_name) 请求。

<a href="" id="identifier--reg-sz-"></a>**标识符** (REG \_ SZ)   
指定端口的名称。 Serenum 读取此值。 提供对 **标识符** 输入值的支持只是为了与某些传统 PCMCIA 设备兼容。 **标识符** 输入值的使用已过时，不应在 Windows 2000 和更高版本中使用驱动程序来实现。 Serenum 返回端口名称以响应 IOCTL \_ Serenum \_ 获取 \_ 端口 \_ 名称请求。

<a href="" id="skipenumerations--reg-dword-"></a>**SkipEnumerations** (REG \_ DWORD)   
在 Windows XP 和更高版本中，此条目值控制 Serenum 何时枚举端口，以响应对 **BusRelations** 的 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](../kernel/irp-mn-query-device-relations.md)请求。 

系统每次生成串行端口设备堆栈时，Serenum 设置用于枚举端口的 *枚举模式* 。 在端口的设备堆栈的初始化过程中，Serenum 的 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程读取端口的 **SkipEnumerations** 入口值并设置枚举模式，如下表所述。

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
<td><p>正常枚举。</p></td>
<td><p>0x00000000</p>
<p> (或值项不存在) </p></td>
<td><p>Serenum 枚举一个串行端口来响应所有 <strong>BusRelations</strong> 请求 (不管是由系统启动还是由用户通过设备管理器或添加硬件向导) 启动。</p></td>
</tr>
<tr class="even">
<td><p>跳过指定数量的枚举。</p></td>
<td><p>从0x00000001 到0xFFFFFFE 的值</p></td>
<td><p>Serenum 会跳过指定数量的枚举，然后在端口保持启用状态的情况下正常枚举。</p></td>
</tr>
<tr class="odd">
<td><p>跳过所有枚举。</p></td>
<td><p>0xFFFFFFFF</p></td>
<td><p>Serenum 从不枚举端口。 必须手动安装连接到端口的设备。</p></td>
</tr>
</tbody>
</table>

例如，如果在系统生成端口设备堆栈时，串行端口的 **SkipEnumerations** 条目值设置为3，则 Serenum 将跳过该端口收到的前三个 **BusRelations** 请求。 只要端口仍处于启用状态，Serenum 随后将以正常方式枚举端口。
