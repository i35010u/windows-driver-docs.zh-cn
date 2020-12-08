---
title: Bug 检查 0xA5 ACPI_BIOS_ERROR
description: ACPI_BIOS_ERROR bug 检查的值为0x000000A5，表示计算机的 ACPI BIOS 与 ACPI 规范不完全兼容。
keywords:
- Bug 检查 0xA5 ACPI_BIOS_ERROR
- ACPI_BIOS_ERROR
ms.date: 09/12/2019
topic_type:
- apiref
api_name:
- ACPI_BIOS_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b56b12fb374b969255edef664e6537874e0218d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784157"
---
# <a name="bug-check-0xa5-acpi_bios_error"></a>Bug 检查0xA5： ACPI \_ BIOS \_ 错误

ACPI \_ BIOS \_ 错误检查的值为0x000000A5。 此 bug 检查表明计算机的高级配置和电源接口 (ACPI) BIOS 与 ACPI 规范不完全兼容。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="acpi_bios_error-parameters"></a>ACPI \_ BIOS \_ 错误参数

参数1指示不兼容的类型。 其他参数的意义取决于参数1的值。

如果 BIOS 不兼容性与即插即用 (PnP) 或电源管理相关，则使用以下参数。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ACPI 的 <strong>deviceExtension</strong></p></td>
<td align="left"><p>ACPI 的 <strong>ResourceList</strong></p></td>
<td align="left"><p><strong>0：</strong> 找不到资源列表</p>
<p><strong>1：</strong> 列表中找不到任何 IRQ 资源</p></td>
<td align="left"><p>ACPI 在启动 ACPI 时，无法在科幻) 向量的资源中找到系统控制中断 (。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p> (参见此页后面的表) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>正在运行的 ACPI 对象</p></td>
<td align="left"><p>来自解释器的返回值</p></td>
<td align="left"><p>以 ULONG 格式 (的控制方法的名称) </p></td>
<td align="left"><p>ACPI 在创建用于表示 ACPI 命名空间的设备扩展时尝试运行控制方法，但此控制方法失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>_PRW 所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法的指针。</p></td>
<td align="left"><p>返回的 <strong>数据类型</strong> (参阅 Amli) </p></td>
<td align="left"><p>ACPI 评估了一个 _PRW，并期望找到一个整数作为包元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>_PRW 所属的 ACPI 扩展</p></td>
<td align="left"><p>Aointer 到 _PRW</p></td>
<td align="left"><p>_PRW 中的元素数</p></td>
<td align="left"><p>ACPI 评估了 _PRW，而返回的包未能包含至少两个元素。 ACPI 规范要求 _PRW 中始终存在两个元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>_PRx 所属的 ACPI 扩展</p></td>
<td align="left"><p>指向 _PRx 的指针</p></td>
<td align="left"><p>一个指针，指向要查找的对象的名称。</p></td>
<td align="left"><p>ACPI 尝试查找命名对象，但找不到该对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>此方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法的指针。</p></td>
<td align="left"><p>返回的 <strong>数据类型</strong> (参阅 Amli) </p></td>
<td align="left"><p>ACPI 评估了一个方法，并期望接收返回的缓冲区。 但是，该方法返回了一些其他数据类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>此方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法的指针。</p></td>
<td align="left"><p>返回的 <strong>数据类型</strong> (参阅 Amli) </p></td>
<td align="left"><p>ACPI 评估了一个方法，并期望接收返回的整数。 但是，该方法返回了一些其他数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>此方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法的指针。</p></td>
<td align="left"><p>返回的 <strong>数据类型</strong> (参阅 Amli) </p></td>
<td align="left"><p>ACPI 计算方法，并期望接收返回的包。 但是，该方法返回了一些其他数据类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>此方法所属的 ACPI 扩展</p></td>
<td align="left"><p>指向方法的指针。</p></td>
<td align="left"><p>返回的 <strong>数据类型</strong> (参阅 Amli) </p></td>
<td align="left"><p>ACPI 计算方法，并期望接收返回的字符串。 但是，该方法返回了一些其他数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>_EJD 所属的 ACPI 扩展</p></td>
<td align="left"><p>解释器返回的状态</p></td>
<td align="left"><p>ACPI 尝试查找的对象的名称</p></td>
<td align="left"><p>ACPI 找不到 _EJD 字符串引用的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ACPI 扩展，ACPI 扩展用于</p></td>
<td align="left"><p>指向 _EJD 方法的指针</p></td>
<td align="left"><p><strong>0：</strong> BIOS 未声明系统为 dockage</p>
<p><strong>1：</strong> 停靠设备的重复设备扩展</p></td>
<td align="left"><p>ACPI 提供了错误或不足的信息，无法提供停靠支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ACPI 需要此对象的 ACPI 扩展</p></td>
<td align="left"><p>ACPI 查找的方法的 (ULONG) 名称</p></td>
<td align="left"><p><strong>0：</strong> 基本情况</p>
<p><strong>1：</strong> 合并</p></td>
<td align="left"><p>ACPI 在命名空间中找不到所需的方法或对象。如果不存在 _HID 或 _ADR，则使用此错误检查代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>ACPI 需要此对象的 NS <strong>PowerResource</strong></p></td>
<td align="left"><p>ACPI 查找的方法的 (ULONG) 名称</p></td>
<td align="left"><p>0： Base case</p></td>
<td align="left"><p>ACPI 在 (或 "device" ) 以外的实体的命名空间中找不到所需的方法或对象。 如果某个电源资源没有 _ON、_OFF 或 _STA，则使用此 bug 检查代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>ACPI 正在分析的当前缓冲区</p></td>
<td align="left"><p>缓冲区的标记</p></td>
<td align="left"><p>缓冲区的指定长度</p></td>
<td align="left"><p>ACPI 无法分析资源描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p> (参见此页后面的表) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p> (参见此页后面的表) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ACPI 正在分析的当前缓冲区</p></td>
<td align="left"><p>缓冲区的标记</p></td>
<td align="left"><p>指向一个变量的指针，该变量包含缓冲区的 ULONGLONG 长度</p></td>
<td align="left"><p>ACPI 无法分析资源描述符。 长度超过了 MAXULONG。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ACPI 计算机语言 (AML) 上下文</p></td>
<td align="left"><p><strong>1：</strong> 未能加载表</p>
<p><strong>2：</strong> 找不到参数路径字符串对象</p>
<p><strong>3：</strong> 未能将参数数据插入 ParameterPath 字符串对象</p>
<p><strong>4：</strong> 系统内存不足</p></td>
<td align="left"><p>NT 状态代码</p></td>
<td align="left"><p>尝试加载表时，ACPI 出现严重错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>指向父 NSOBJ 的指针</p></td>
<td align="left"><p>指向非法子 ACPI 命名空间对象的指针</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>在处理 xSDT 时，ACPI 出现严重错误。 对象被声明为不能有子级的父级的子级。</p></td>
</tr>
</tbody>
</table>

 

如果中断路由故障或发生不兼容，则使用以下参数。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p><strong>InterruptModel</strong> (整数) </p></td>
<td align="left"><p>来自解释器的返回值</p></td>
<td align="left"><p>指向 PIC 控件方法的指针</p></td>
<td align="left"><p>ACPI 试图计算 PIC 控制方法但失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10001</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>指向设备对象的父级的指针</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p> (参阅以下注释部分) </p></td>
<td align="left"><p>ACPI 尝试进行中断路由，但失败了。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10002</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>指向 ACPI 正在查找但找不到的字符串名称的指针</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p> (参阅以下注释部分) </p></td>
<td align="left"><p>ACPI 找不到 _PRT 中引用的链接节点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10003</p></td>
<td align="left"><p>指向设备对象的指针</p></td>
<td align="left"><p>设备 ID 或功能号。</p>
<p>此 DWORD 编码如下： bits 5:0 是 PCI 设备号，而 bits 8:6 是 PCI 函数号</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p> (参阅以下注释部分) </p></td>
<td align="left"><p>ACPI 在设备的 _PRT 包中找不到映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10005</p></td>
<td align="left"><p>指向 _PRT 对象的指针</p>
<p> (参阅以下注释部分) </p></td>
<td align="left"><p>指向当前 _PRT 元素的指针。</p>
<p> (此指针是 _PRT 中的索引。 ) </p></td>
<td align="left"><p>设备 ID 或功能号。</p>
<p>此 DWORD 编码如下： bits 15:0 是 PCI 函数号，位31:16 是 PCI 设备号</p></td>
<td align="left"><p>ACPI 在 _PRT 中找到了函数 ID 并不是全部 F 的条目。</p>
<p>_PRT 条目 (通用格式是指定了设备号，但函数号不是。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10006</p></td>
<td align="left"><p>指向链接节点的指针。</p>
<p> (此设备缺少 _DIS 方法。 ) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 找到了一个链接节点，但无法禁用该节点。</p>
<p>若要允许 reprogramming，必须禁用 (链接节点。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10007</p></td>
<td align="left"><p>找不到的矢量</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>_PRT 包含对某个向量的引用，该引用未在 i/o APIC 项的 MAPIC 表中描述。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10008</p></td>
<td align="left"><p>无效的中断级别。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 科幻中断级别无效。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10009</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>找不到 FADT) 的固定 ACPI 说明表 (。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无法找到根系统说明指针 (RSDP) 或扩展系统说明表 (XSDT) </p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000B</p></td>
<td align="left"><p>ACPI 表签名</p></td>
<td align="left"><p>指向 ACPI 表的指针</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 表的长度与表修订版本不一致。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000C</p></td>
<td align="left"><p>修订 ID</p></td>
<td align="left"><p>函数索引</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>中断的 _DSM 方法返回了格式不正确的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000D</p></td>
<td align="left"><p>设备的 ACPI 扩展</p></td>
<td align="left"><p>值0： _PRW 指定，但没有支持唤醒的中断和至少一个 GPIO 中断值1：由于存在可唤醒的中断，_PRW 应将 GpeInfo 值指定为0xffffffff</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>设备使用了 GPE 和 GPIO 中断，这是不受支持的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000E</p></td>
<td align="left"><p></p>验证函数返回的状态。</td>
<td align="left"><p> 指向 ACPI 命名空间路径 UNICODE_STRING 的指针。</p></td>
<td align="left"><p>与 SDEV 进行比较的资源列表指针。</p></td>
<td align="left"><p>安全设备的 SDEV 资源与其相应的 _CRS 或 _PRS 条目不匹配。</p></td>
</tr>
</tbody>
</table>

如果发生了其他故障或不兼容性，则使用以下参数。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定表中的 i/o 端口</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>"固定 ACPI 说明" 表中的 PM_TMR_BLK 条目不指向工作 ACPI 计时器块。</p></td>
</tr>
</tbody>
</table>

此表描述了使用以下参数的内存使用情况问题。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>内存区域物理地址的高部分。</p></td>
<td align="left"><p>内存区域物理地址的低部分。</p></td>
<td align="left"><p>要映射的内存长度。</p></td>
<td align="left"><p>在处理内存操作区域时，ACPI 出现严重错误。 内存操作区域尝试映射已分配给 OS 使用的内存。</p></td>
</tr>
</tbody>
</table>


如果参数1等于 **0x02**，则 ACPI BIOS 无法处理 PCI 根总线的资源列表。 在这种情况下，参数3指定了确切的问题，其余的参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>指向 QUERY_RESOURCES IRP 的指针</p></td>
<td align="left"><p>ACPI 无法将 BIOS 的资源列表转换为正确的格式。 这可能表示 BIOS "列表编码过程中出现错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>指向 QUERY_RESOURCE_REQUIREMENTS IRP 的指针</p></td>
<td align="left"><p>ACPI 无法将 BIOS 的资源列表转换为正确的格式。 这可能表示 BIOS "列表编码过程中出现错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 发现空的资源列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>0x3</p></td>
<td align="left"><p>指向 PNP CRS 描述符的指针</p></td>
<td align="left"><p>ACPI 在 CRS 中找不到当前总线号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI 总线的 ACPI 扩展</p></td>
<td align="left"><p>指向 PCI 的资源列表的指针</p></td>
<td align="left"><p>指向 E820 内存表的指针</p></td>
<td align="left"><p>PCI 声明要解码的资源的列表与 E820 BIOS 接口报告的内存区域列表重叠。 永远不允许 (此类冲突。 ) </p></td>
</tr>
</tbody>
</table>

 

如果参数1等于 **0x10**，则 ACPI BIOS 无法正确确定系统到设备的映射。 在这种情况下，参数3指定了确切的问题，其余的参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>需要其映射的 ACPI 扩展</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>此 DEVICE_POWER_STATE (为 "x + 1" ) </p></td>
<td align="left"><p>_PRx 映射回不支持的 S 状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>需要其映射的 ACPI 扩展</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>无法映射的 SYSTEM_POWER_STATE</p></td>
<td align="left"><p>ACPI 找不到要与 S 状态关联的 D 状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>需要其映射的 ACPI 扩展</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>无法映射的 SYSTEM_POWER_STATE</p></td>
<td align="left"><p>设备声称当系统处于这种状态时，可以唤醒系统，但系统并不真正支持这种状态。</p></td>
</tr>
</tbody>
</table>

 

如果参数1等于 **0x11**，则系统无法进入 ACPI 模式。 在这种情况下，参数2指定了确切的问题，其余的参数具有以下定义。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
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
<td align="left"><p>系统无法分配关键驱动程序结构。</p></td>
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
<td align="left"><p>系统无法加载 DDBs。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>系统无法连接中断向量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不会在 PM1 控制寄存器中设置 SCI_EN。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>指向具有错误校验和的表的指针</p></td>
<td align="left"><p>创建者修订版</p></td>
<td align="left"><p>表校验和不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>指向无法加载 ACPI 的表的指针</p></td>
<td align="left"><p>创建者修订版</p></td>
<td align="left"><p>ACPI 无法加载 DDB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>FADT 版本</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固件版本不受支持。</p></td>
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
<td align="left"><p>系统在 MADT 中找不到任何有效的本地 SAPIC 结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数1的值指示错误。

<a name="resolution"></a>解决方法
----------

如果正在调试此错误，请使用 [**！分析-v**](-analyze.md) 扩展。 此扩展显示 (设备扩展或 nsobjects 的所有相关数据，或与特定错误) 相关的任何数据。

如果未执行调试，此错误表示必须获取新的 BIOS。 联系你的供应商或访问 internet 以获取新的 BIOS。

如果无法获取更新的 BIOS，或最新的 BIOS 仍不符合 ACPI 标准，你可以在文本模式安装过程中关闭 ACPI 模式。 若要关闭 ACPI 模式，请在系统提示你安装存储驱动程序时按 F7 键。 系统不会通知你按下了 F7 键，但它会以静默方式禁用 ACPI，并使你能够继续安装。

<a name="remarks"></a>备注
-------

PCI 路由表 (\_ PRT) 为 ACPI BIOS 对象，该对象指定如何将所有 PCI 设备连接到中断控制器。 具有多个 PCI 总线的计算机可能具有多个 \_ prt。

可以 \_ 在调试器中显示 PRT，方法是结合使用 **！ acpikd** 和 \_ PRT 对象的地址作为其参数。

 

 




