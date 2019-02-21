---
title: 指定高级属性页的配置参数
description: 指定的高级的属性页配置参数
ms.assetid: 9c243edb-f667-4244-8de2-8335fac43220
keywords:
- 添加注册表部分网络 WDK，高级的属性页上配置
- 高级的属性页上配置 WDK 网络
- 参数 WDK 网络
- 配置参数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23871adec26ce24496924927c391ed62cdeebdce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520779"
---
# <a name="specifying-configuration-parameters-for-the-advanced-properties-page"></a>指定的高级的属性页配置参数

> [!NOTE]
> 在 Windows 10，版本 1703 之前, 驱动程序升级和 Windows 更新可能导致更改为驱动程序以前已在中定义的 INF 值**高级**属性页。
> 从 Windows 10，版本 1703，开始一个驱动程序指定其 INF 文件中的高级的属性通过持久保留这些更新。



安装网络组件 （适配器） 的 INF 文件可以指定在显示的适配器配置参数**高级**组件的属性页。 在用户指定的配置值**高级**属性页写入到组件的根实例键。

请注意，如果适配器支持**高级**属性页**特征**中的条目*DDInstall*部分适配器必须包括 NCF\_HAS\_UI 值。

网络 INF 文件中通过高级页指定显示的配置参数*添加注册表部分*引用*DDInstall*组件部分。 此类*添加注册表部分*添加到一个或多个配置子项**Ndi\\params**密钥。 格式为配置参数子项**Ndi\\params\\**<em>SubKeyName</em>，其中*SubKeyName*是 REG\_SZ指定特定于供应商的参数名称的值。 例如，可命名为一个参数，指定收发器类型的键**Ndi\\params\\TransceiverType**。

以下关键字是保留和不能用作**Ndi\\params\\**<em>SubKeyName</em>:**BundleId**， **BusType**，**特征**， **ComponentId**，**说明**， **DeviceInstanceId**， **DriverDate**， **DriverDesc**， **DriverVersion**， **InfPath**， **InfSection**， **InfSectionExt**，* * *IfType** **InstallTimeStamp**，**制造商**，* * *MediaType*<em>，**NetCfgInstanceId</em>*，**NetLuidIndex*<em>，</em>*  *PhysicalMediaType*<em>，* * 提供程序</em><em>，和 **ProviderName</em>*。

添加到每个参数子项**Ndi\\params**，则*添加注册表部分*必须添加**ParamDesc**（参数说明） 和**类型**值。 *添加注册表部分*还可以添加**默认**并**可选**参数的值和参数是数值，如果**最小值**，**最大**，并**步骤**值。 下表描述了可以添加到每个值**Ndi\\params**密钥。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名称</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ParamDesc</p></td>
<td align="left"><p><em>String</em></p></td>
<td align="left"><p>参数上的显示名称<strong>高级</strong>页</p></td>
</tr>
<tr class="even">
<td align="left"><p>在任务栏的搜索框中键入</p></td>
<td align="left"><p><strong>int</strong>，<strong>长</strong>， <strong>Word</strong>， <strong>dword</strong>，<strong>编辑</strong>，或<strong>枚举</strong></p></td>
<td align="left"><p>参数的类型： <strong>int</strong>，<strong>长</strong>， <strong>Word</strong>，以及<strong>dword</strong>指定数字的参数;<strong>编辑</strong>并<strong>枚举</strong>指定一个文本参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>默认</p></td>
<td align="left"><p><em>default value</em></p></td>
<td align="left"><p>参数的默认值： 适用于数值参数必须是数字值 ( <strong>int</strong>，<strong>长</strong>， <strong>Word</strong>，或者<strong>dword</strong>) 相匹配指定的参数类型;对于文本参数，必须是字符串。 必须指定所需参数的默认值。 此外可以为可选参数指定默认值。 当用户选择的选项为可选参数输入值时，默认值，如果指定，会显示该参数的编辑框中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><strong>0</strong>或<strong>1</strong></p></td>
<td align="left"><p></p>
<strong>0</strong>必需。 指定参数的值或使用默认值。
<strong>1</strong>可选。 可以将标记<strong>不存在</strong>上<strong>高级</strong>页。</td>
</tr>
<tr class="odd">
<td align="left"><p>最小</p></td>
<td align="left"><p><em>数字值</em></p></td>
<td align="left"><p>数值参数的最小值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>最大</p></td>
<td align="left"><p><em>数字值</em></p></td>
<td align="left"><p>数值参数的最大值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>步骤</p></td>
<td align="left"><p><em>数字值</em></p></td>
<td align="left"><p>步骤 （间隔） 之间的数字参数的有效值。 最小值是起始点。</p></td>
</tr>
</tbody>
</table>

 

值范围**枚举**参数指定了一个子项具有以下格式：

**Ndi\\params\\**<em>SubKeyName</em>**\\enum**

每个枚举的值必须具有一个子项。 每个**枚举**子项指定数字值 （以开头的第一个枚举值为零） 和值的说明。

以下是一种*添加注册表部分*，它将一个名为的配置参数**TransType**。

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

 

 





