---
title: Bug 检查 0xA5 ACPI_BIOS_ERROR
description: ACPI_BIOS_ERROR bug 检查具有值，该值指示在 ACPI BIOS 的计算机不是完全符合 ACPI 规范 0x000000A5。
ms.assetid: f0366a3c-a2c4-4fc8-a722-52fdda59eb2b
keywords:
- Bug 检查 0xA5 ACPI_BIOS_ERROR
- ACPI_BIOS_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACPI_BIOS_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 050a654f4c9865f0ca2ea8ceb8f4f2be6c66903c
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464181"
---
# <a name="bug-check-0xa5-acpibioserror"></a>Bug 检查 0xA5：ACPI\_BIOS\_ERROR


ACPI\_BIOS\_错误 bug 检查的值为 0x000000A5。 此 bug 对勾指示高级配置和电源接口 (ACPI) BIOS 的计算机不是完全符合 ACPI 规范。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="acpibioserror-parameters"></a>ACPI\_BIOS\_错误参数


参数 1 表示不兼容的类型。 其他参数的含义取决于参数 1 的值。

如果与插即用 (PnP) 或电源管理相关的 BIOS 不兼容，则使用以下参数。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ACPI 的<strong>deviceExtension</strong></p></td>
<td align="left"><p>ACPI 的<strong>ResourceList</strong></p></td>
<td align="left"><p><strong>0:</strong>没有找到任何资源的列表</p>
<p><strong>1:</strong>在列表中不找到任何 IRQ 资源</p></td>
<td align="left"><p>ACPI 找不到 ACPI 启动时传递给它的资源中的系统管理中断 (SCI) 向量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>（请参阅表更高版本在此页）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>正在运行 ACPI 对象</p></td>
<td align="left"><p>从解释器返回的值</p></td>
<td align="left"><p>控制方法 （在 ULONG 格式） 的名称</p></td>
<td align="left"><p>ACPI 尝试运行控制方法，同时创建设备扩展来表示 ACPI 名称空间，但此控件方法失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>ACPI 扩展该 _PRW 属于</p></td>
<td align="left"><p>指向方法</p></td>
<td align="left"><p><strong>数据类型</strong>返回 （请参阅 Amli.h）</p></td>
<td align="left"><p>ACPI 计算 _PRW 并在需要查找 package 元素作为一个整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>ACPI 扩展该 _PRW 属于</p></td>
<td align="left"><p>到 _PRW Aointer</p></td>
<td align="left"><p>_PRW 中的元素数</p></td>
<td align="left"><p>ACPI 评估 _PRW 和包返回了无法包含至少两个元素。 ACPI 规范要求两个元素始终为 _PRW 中存在。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ACPI 扩展该 _PRx 属于</p></td>
<td align="left"><p>指向 _PRx</p></td>
<td align="left"><p>指向要查找的对象的名称</p></td>
<td align="left"><p>ACPI 曾尝试找不到命名的对象，但它找不到对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>该方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法</p></td>
<td align="left"><p><strong>数据类型</strong>返回 （请参阅 Amli.h）</p></td>
<td align="left"><p>ACPI 计算方法，并应接收缓冲区中返回。 但是，该方法返回某些其他数据类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>该方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法</p></td>
<td align="left"><p><strong>数据类型</strong>返回 （请参阅 Amli.h）</p></td>
<td align="left"><p>ACPI 计算方法，并应接收一个整数返回。 但是，该方法返回某些其他数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>该方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法</p></td>
<td align="left"><p><strong>数据类型</strong>返回 （请参阅 Amli.h）</p></td>
<td align="left"><p>ACPI 计算方法，并应接收包返回的。 但是，该方法返回某些其他数据类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>该方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法</p></td>
<td align="left"><p><strong>数据类型</strong>返回 （请参阅 Amli.h）</p></td>
<td align="left"><p>ACPI 计算方法，并应接收一个字符串返回。 但是，该方法返回某些其他数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>ACPI 扩展该 _EJD 属于</p></td>
<td align="left"><p>解释器返回的状态</p></td>
<td align="left"><p>ACPI 尝试查找的对象的名称</p></td>
<td align="left"><p>ACPI 找不到 _EJD 字符串引用的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ACPI 找到停靠设备的 ACPI 扩展</p></td>
<td align="left"><p>指向 _EJD 方法</p></td>
<td align="left"><p><strong>0:</strong>BIOS 不会声称系统是 dockage</p>
<p><strong>1:</strong>重复的设备的扩展停靠设备</p></td>
<td align="left"><p>ACPI 提供停靠支持的问题或者没有足够信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ACPI 扩展 ACPI 所需的对象</p></td>
<td align="left"><p>ACPI 查找的方法 (ULONG) 名称</p></td>
<td align="left"><p><strong>0:</strong>基本用例</p>
<p><strong>1:</strong>冲突</p></td>
<td align="left"><p>ACPI 找不到所需的方法或对象中的命名空间，如果没有 _HID 或 _ADR 存在，则使用此 bug 检查代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NS <strong>PowerResource</strong> ACPI 需要的对象</p></td>
<td align="left"><p>ACPI 查找的方法 (ULONG) 名称</p></td>
<td align="left"><p>0:基本用例</p></td>
<td align="left"><p>ACPI 找不到所需的方法或对象的命名空间中的 power 资源 （或"设备"之外的实体）。 如果没有 _ON，_OFF 或 _STA power 资源存在，则使用此 bug 检查代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>ACPI 分析当前缓冲区</p></td>
<td align="left"><p>缓冲区的标记</p></td>
<td align="left"><p>指定的长度的缓冲区</p></td>
<td align="left"><p>ACPI 无法分析资源描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>（请参阅表更高版本在此页）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>（请参阅表更高版本在此页）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ACPI 分析当前缓冲区</p></td>
<td align="left"><p>缓冲区的标记</p></td>
<td align="left"><p>指向包含缓冲区的 ULONGLONG 长度的变量的指针</p></td>
<td align="left"><p>ACPI 无法分析资源描述符。 长度超过 MAXULONG。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ACPI 机器语言 (AML) 上下文</p></td>
<td align="left"><p><strong>1:</strong>无法加载表</p>
<p><strong>2:</strong>找不到参数路径字符串对象</p>
<p><strong>3:</strong>无法将参数数据插入到 ParameterPath 字符串对象</p>
<p><strong>4:</strong>系统内存不足</p></td>
<td align="left"><p>NT 状态代码</p></td>
<td align="left"><p>尝试加载的表时，ACPI 发生了严重错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>指向父 NSOBJ</p></td>
<td align="left"><p>指向非法子 ACPI 命名空间对象的指针</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>ACPI 处理 xsdt 表已有一个致命错误。 对象声明为不能具有子级的父级的子级。</p></td>
</tr>
</tbody>
</table>

 

如果发生中断路由故障或不兼容，则使用以下参数。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p><strong>InterruptModel</strong> （整数）</p></td>
<td align="left"><p>从解释器返回的值</p></td>
<td align="left"><p>指向 PIC 控制方法的指针</p></td>
<td align="left"><p>ACPI 尝试评估 PIC 控制方法，但失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10001</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>指向设备对象的父对象的指针</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p>（请参阅以下评论部分）</p></td>
<td align="left"><p>ACPI 尝试执行中断路由，但失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10002</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>指向 ACPI 查找，但找不到的字符串名称</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p>（请参阅以下评论部分）</p></td>
<td align="left"><p>ACPI 找不到 _PRT 中引用的链接节点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10003</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>设备 ID 或函数数。</p>
<p>按如下所示编码此 DWORD: 5:0 位均为 PCI 设备号，和 bits 8:6 PCI 函数多</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p>（请参阅以下评论部分）</p></td>
<td align="left"><p>ACPI 找不到映射 _PRT 包中的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10005</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p>（请参阅以下评论部分）</p></td>
<td align="left"><p>指向当前 _PRT 元素的指针。</p>
<p>（此指针是 _PRT 的索引。）</p></td>
<td align="left"><p>设备 ID 或函数数。</p>
<p>按如下所示编码此 DWORD: bits 15:0 PCI 函数号，且位 31:16 PCI 设备数</p></td>
<td align="left"><p>ACPI 函数 ID 不是全部为 F 的 _PRT 中找到一个条目。</p>
<p>（_PRT 条目的一般格式是指定设备号，但不是函数号）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10006</p></td>
<td align="left"><p>指向链接节点的指针。</p>
<p>（此设备缺少 _DIS 方法）。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 找到链接节点，但它不能禁用节点。</p>
<p>（链接节点必须禁用以允许重新编程。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10007</p></td>
<td align="left"><p>未找到向量</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>_PRT 包含对 I/O APIC 条目 MAPIC 表中未描述的矢量的引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10008</p></td>
<td align="left"><p>无效的中断级别中。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 名工商管理学博士中断级别无效。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10009</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>找不到固定 ACPI 描述表 (FADT)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>未能找到根系统说明指针 (RSDP) 或扩展系统说明表 （xsdt 表）</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000B</p></td>
<td align="left"><p>ACPI 表签名</p></td>
<td align="left"><p>指向 ACPI 表</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 表的长度不是与表修订版本一致的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定表中的 I/O 端口</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固定的 ACPI 描述表中的 PM_TMR_BLK 条目未指向工作 ACPI 计时器块。</p></td>
</tr>
</tbody>
</table>

 

如果发生其他故障或不兼容，则使用以下参数。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定表中的 I/O 端口</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固定的 ACPI 描述表中的 PM_TMR_BLK 条目没有指向工作 ACPI 计时器块。</p></td>
</tr>
</tbody>
</table>

 

如果参数 1 等于**0x02**，ACPI BIOS 无法处理 PCI 根总线的资源列表。 在这种情况下，参数 3 指定确切的问题，以及剩余参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>适用于 PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>指向 QUERY_RESOURCES IRP 的指针</p></td>
<td align="left"><p>ACPI 不能将 BIOS' 资源列表转换为正确格式。 这可能表示在编码过程的 BIOS 的列表中的错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>适用于 PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>指向 QUERY_RESOURCE_REQUIREMENTS IRP 的指针</p></td>
<td align="left"><p>ACPI 不能将 BIOS' 资源列表转换为正确格式。 这可能表示在编码过程的 BIOS 的列表中的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>适用于 PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 找到空的资源列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>适用于 PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x3</p></td>
<td align="left"><p>指向的即插即用 CRS 描述符的指针</p></td>
<td align="left"><p>ACPI 中 CRS 中找不到当前的总线数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>适用于 PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>一个指向 PCI 资源列表</p></td>
<td align="left"><p>指向 E820 内存表</p></td>
<td align="left"><p>E820 BIOS 接口报告的内存区域的列表与重叠的 PCI 声明要解码的资源的列表。 （这种冲突，则永远不会允许。）</p></td>
</tr>
</tbody>
</table>

 

如果参数 1 等于**0x10**，ACPI BIOS 无法确定系统-到-设备的状态正确映射。 在此情况下，参数 3 指定确切的问题，以及剩余参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACPI 扩展所需的映射</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>DEVICE_POWER_STATE (这是"x + 1")</p></td>
<td align="left"><p>_PRx 恢复到不受支持 S 状态映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACPI 扩展所需的映射</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>不能映射 SYSTEM_POWER_STATE</p></td>
<td align="left"><p>ACPI 找不到可将与 S 状态相关联的 D 状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ACPI 扩展所需的映射</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>不能映射 SYSTEM_POWER_STATE</p></td>
<td align="left"><p>设备声明，以便能够将系统唤醒时系统处于此 S 状态，但系统实际上并不支持此 S 状态。</p></td>
</tr>
</tbody>
</table>

 

如果参数 1 等于**0x11**，系统可能会进入 ACPI 模式。 在此情况下，参数 2 指定确切的问题，以及剩余参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法初始化 AML 解释器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统找不到 RSDT。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法分配必需的驱动程序结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法加载 RSDT。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法加载 Ddb。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法连接中断矢量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>SCI_EN 永远不会变得 PM1 控制寄存器中设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>指向具有错误的校验和的表</p></td>
<td align="left"><p>创建者修订</p></td>
<td align="left"><p>表校验和不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>指向 ACPI 未能加载表</p></td>
<td align="left"><p>创建者修订</p></td>
<td align="left"><p>ACPI 加载 DDB 失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>FADT 版本</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不受支持的固件版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统找不到 MADT。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>在系统中未找到任何有效的本地 SAPIC 结构 MADT。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数 1 的值指示的错误。

<a name="resolution"></a>分辨率
----------

如果要调试此错误，使用[ **！ 分析-v** ](-analyze.md)扩展。 此扩展将显示所有相关的数据 （设备扩展、 nsobjects，或任何适合于特定的错误）。

如果您执行的不调试，此错误表示，您必须获取新的 BIOS。 请联系你的供应商或访问 internet 来获取新的 BIOS。

如果无法获取更新的 BIOS 或最新的 BIOS 仍不符合 ACPI，可以关闭 ACPI 模式在文本模式下安装过程。 若要禁用 ACPI 模式，请按 F7 键时系统会提示您安装存储驱动程序。 F7 键已按下，但它以无提示方式禁用 ACPI 并使你能够继续您的安装，系统不会通知您。

<a name="remarks"></a>备注
-------

PCI 路由表 (\_PRT) 是 ACPI BIOS 对象，指定如何所有 PCI 设备都连接到中断控制器。 具有多个 PCI 总线的计算机可能有多个\_Prt。

可以显示\_通过使用在调试器中的 PRT **！ acpikd.nsobj**扩展的地址以及\_PRT 对象作为其参数。

 

 




