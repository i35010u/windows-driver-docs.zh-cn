---
title: 为 "高级属性" 页指定配置参数
description: 指定高级属性页的配置参数
keywords:
- 添加-注册表-WDK 网络，高级属性页面配置
- 高级属性页配置 WDK 网络
- 参数 WDK 网络
- 配置参数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19ff6486150c05cc72130d38bea870c0d1e9eded
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790435"
---
# <a name="specifying-configuration-parameters-for-the-advanced-properties-page"></a>指定高级属性页的配置参数

> [!NOTE]
> 在 Windows 10 之前的版本1703中，驱动程序升级和 Windows 更新可能会导致对驱动程序之前在 " **高级** 属性" 页中定义的 INF 值进行更改。
> 从 Windows 10 版本1703开始，驱动程序在其 INF 文件中指定的高级属性可通过这些更新来保存。



一个 INF 文件，用于安装 (适配器的网络组件) 可以指定适配器配置参数以在组件的 " **高级** 属性" 页中显示。 用户在 " **高级** 属性" 页中指定的配置值将写入组件的根实例键。

请注意，如果适配器支持 **高级** 属性页面，则适配器的 *DDInstall* 部分中的 "**特征**" 条目必须包含 "NCF" \_ 具有 \_ UI 值。

网络 INF 文件通过 *DDInstall* 部分为组件引用的 "*添加注册表" 部分* 指定要在 "高级" 页中显示的配置参数。 此类 *添加注册表部分* 将一个或多个配置子项添加到 **Ndi \\ params** 键。 配置参数子项的格式为 **Ndi \\ params \\**<em>SubKeyName</em>，其中 *SubKeyName* 是 \_ 指定供应商特定参数名称的 REG SZ 值。 例如，指定一个收发器类型的参数的键可以命名为 **Ndi \\ params \\ TransceiverType**。

以下关键字是保留关键字，不能用作 **Ndi \\ \\ params**<em>SubKeyName</em>： **BundleId**、 **BusType**、**特性**、**组件** 器、**说明**、 **DeviceInstanceId**、 **DriverDate**、 **DriverDesc**、 **DriverVersion**、 **InfPath**、 **InfSection**、 **InfSectionExt**、IfType、InstallTimeStamp *、* *  **InstallTimeStamp****制造商**、* * 媒体 id *MediaType*<em>、**NetCfgInstanceId</em>*、**NetLuidIndex*<em>、</em> *  *PhysicalMediaType*<em>、* * 提供程序</em><em>和 **ProviderName</em>*。

对于添加到 **Ndi \\ params** 的每个参数子项，"*添加注册表" 部分* 必须) 和 **类型** 值添加 **ParamDesc** (参数说明。 如果参数是数值、**最小** 值、**最大** 值和 **步长** 值，则 "*外接程序" 部分* 还可以为参数添加 **默认** 值和 **可选** 值。 下表描述了可添加到每个 **Ndi \\ 参数** 键的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“属性”</th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ParamDesc</p></td>
<td align="left"><p><em>字符串</em></p></td>
<td align="left"><p>在 " <strong>高级</strong> " 页上为参数显示的名称</p></td>
</tr>
<tr class="even">
<td align="left"><p>类型</p></td>
<td align="left"><p><strong>int</strong>、 <strong>long</strong>、 <strong>Word</strong>、 <strong>dword</strong>、 <strong>edit</strong>或 <strong>enum</strong></p></td>
<td align="left"><p>参数的类型： <strong>int</strong>、 <strong>long</strong>、 <strong>Word</strong>和 <strong>dword</strong> 指定数值参数; <strong>edit</strong> 和 <strong>enum</strong> 指定文本参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>默认</p></td>
<td align="left"><p><em>默认值</em></p></td>
<td align="left"><p>参数的默认值：对于数值参数，必须是与指定参数类型匹配 ( <strong>int</strong>、 <strong>long</strong>、 <strong>Word</strong>或 <strong>dword</strong>) 的数值;对于文本参数，必须为字符串。 必须为所需参数指定默认值。 还可以为可选参数指定默认值。 当用户选择输入可选参数值的选项时，默认值（如果已指定）会显示在该参数的编辑框中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><strong>0</strong> 或 <strong>1</strong></p></td>
<td align="left"><p></p>
<strong>0</strong> 是必需的。 指定参数的值，或使用默认值。
<strong>1</strong> 可选。 可以在 "<strong>高级</strong>" 页上标记为 "<strong>不存在</strong>"。</td>
</tr>
<tr class="odd">
<td align="left"><p>Min</p></td>
<td align="left"><p><em>数值</em></p></td>
<td align="left"><p>数值参数的最小值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Max</p></td>
<td align="left"><p><em>数值</em></p></td>
<td align="left"><p>数值参数的最大值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>步骤</p></td>
<td align="left"><p><em>数值</em></p></td>
<td align="left"><p>单步 (数值参数的有效值之间) 。 最小值为开始点。</p></td>
</tr>
</tbody>
</table>

 

**枚举** 参数的值范围是使用具有以下格式的子项指定的：

**Ndi \\ params \\**<em>SubKeyName</em>**\\ 枚举**

每个枚举值必须具有一个子项。 每个 **enum** 子项均指定一个数值 (从零开始) 第一个枚举值的值和该值的说明。

下面是添加一个名为 **TransType** 的配置参数的 "*添加注册表" 部分* 的示例。

```INF
[a1.params.reg]
HKR, Ndi\params\TransType,      ParamDesc, 0, "Transceiver Type"
HKR, Ndi\params\TransType,      Type,      0, "enum"
HKR, Ndi\params\TransType,      Default,   0, "0"
HKR, Ndi\params\TransType,      Optional,  0, "0"
HKR, Ndi\params\TransType\enum, "0",       0, "Auto-Connector"
HKR, Ndi\params\TransType\enum, "1",       0, "Thick Net(AUI/DIX)"
HKR, Ndi\params\TransType\enum, "2",       0, "Thin Net (BNC/COAX)"
HKR, Ndi\params\TransType\enum, "3",       0, "Twisted-Pair (TPE)"
```

 

 





