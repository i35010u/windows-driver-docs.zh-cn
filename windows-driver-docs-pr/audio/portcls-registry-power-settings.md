---
title: PortCls 注册表电源设置
description: 本主题说明了 Windows 8 的 PortCls 注册表电源设置。
ms.assetid: 148D044E-B736-4526-BDC5-2C180A590C21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 434a1e10747edb83b8deb74a14d9b45bc2257f4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328765"
---
# <a name="portcls-registry-power-settings"></a>PortCls 注册表电源设置


本主题说明了 Windows 8 的 PortCls 注册表电源设置。

在 Windows 8 中，(PortCls) 微型端口驱动程序可以使用注册表值在驱动程序的注册表项中要执行以下操作：

-   确定 PortCls 启用空闲处理能力管理

-   确定电池节省模式，与高性能模式的空闲超时值

默认情况下，Windows 8 具有 PortCls 使用来确定是否注册为"空闲设备"检测使用电源管理器，当运行时电源框架指示不再需要 power 的电源设置。 用于描述电源设置配置文件的参数定义，如下所示。

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
<td align="left">0 秒的超时。</td>
</tr>
<tr class="even">
<td align="left">IdlePowerState</td>
<td align="left">REG_BINARY</td>
<td align="left">3 (D3)
<p>有效值：</p>
1 - D1 2 - D2 3 - D3</td>
<td align="left">指定设备将不再需要 power 时输入的电源状态。</td>
</tr>
<tr class="odd">
<td align="left">PerformanceIdleTime</td>
<td align="left">REG_BINARY</td>
<td align="left">0</td>
<td align="left">0 秒的超时。</td>
</tr>
</tbody>
</table>

 

以下 Windows 注册表片段演示的语法，用于提供电源设置信息。

``` syntax
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4D36E96C-E325-11CE-BFC1-08002BE10318}\0000\PowerSettings]
"ConservationIdleTime"=hex:1e,00,00,00
"PerformanceIdleTime"=hex:00,00,00,00
“IdlePowerState”=hex:03,00,00,00
```

前面的片段显示了"1e"十六进制 （十六进制） 值*ConservationIdleTime*，这相当于 30 秒的空闲超时和。 "0"，显示的十六进制值*PerformanceIdleTime*意味着空闲管理已被禁用。 和的值"03"所示*IdlePowerState*意味着当不再需要 power，与此电源设置配置文件关联的设备将进入 D3 电源状态。

 

 




