---
title: PortCls 注册表电源设置
description: 本主题说明适用于 Windows 8 的 PortCls 注册表电源设置。
ms.assetid: 148D044E-B736-4526-BDC5-2C180A590C21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e17fd64b7e2ff977bb5b2a470e919eefd7c8b4dd
ms.sourcegitcommit: 1addd14b2063aba321f5428a23393f22f59c02b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035717"
---
# <a name="portcls-registry-power-settings"></a>PortCls 注册表电源设置


本主题说明适用于 Windows 8 的 PortCls 注册表电源设置。

在 Windows 8 中，（PortCls）微型端口驱动程序可以使用驱动程序的注册表项中的注册表值来执行以下操作：

- 确定 PortCls 是否启用空闲电源管理

- 确定电池保留模式和高性能模式的空闲超时值

默认情况下，Windows 8 具有电源设置，PortCls 使用它来确定是否使用电源管理器注册 "设备空闲" 检测，而运行时电源框架指示不再需要电源。 用于描述电源设置配置文件的参数的定义如下。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表值</th>
<th align="left">数据类型</th>
<th align="left">默认值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ConservationIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0秒超时。</td>
</tr>
<tr class="even">
<td align="left">IdlePowerState</td>
<td align="left">REG_BINARY</td>
<td align="left">3（D3）
<p>有效值：</p>
1-D1 2-D2 3-D3</td>
<td align="left">指定当不再需要电源时设备将进入的电源状态。</td>
</tr>
<tr class="odd">
<td align="left">PerformanceIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0秒超时。</td>
</tr>
</tbody>
</table>

 

以下 Windows 注册表片段显示了用于提供电源设置信息的语法。

``` syntax
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4D36E96C-E325-11CE-BFC1-08002BE10318}\0000\PowerSettings]
"ConservationIdleTime"=hex:1e,00,00,00
"PerformanceIdleTime"=hex:00,00,00,00
"IdlePowerState"=hex:03,00,00,00
```

前面的片段显示了*ConservationIdleTime*的十六进制（十六进制）值 "1e"，这相当于30秒的空闲超时。 为*PerformanceIdleTime*显示的十六进制值 "0" 表示已禁用空闲管理。 为*IdlePowerState*显示的 "03" 值表示当不再需要电源时，与此电源设置配置文件关联的设备将进入 D3 电源状态。
