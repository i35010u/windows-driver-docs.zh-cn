---
title: 网络 INF 文件中的 DDInstall 节
description: 网络 INF 文件中的 DDInstall 节
ms.assetid: f6621796-0d1f-4d96-9850-720718e7ac44
keywords:
- INF 文件 WDK network，DDInstall 部分
- 网络 INF 文件 WDK，DDInstall 部分
- DDInstall 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dc8ffe2ea0d1867c6fea150c7a63a61bd279c26
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212203"
---
# <a name="ddinstall-section-in-a-network-inf-file"></a>网络 INF 文件中的 DDInstall 节





网络 INF 文件中的 *DDInstall* 部分基于通用 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)。

网络 INF 文件中的 *DDInstall* 部分具有以下特定于网络的条目：

-   [特征](#characteristics)
-   [BusType](#bustype)
-   [Port1DeviceNumber 和 Port1FunctionNumber](#port1devicenumber-and-port1functionnumber)

### <a name="characteristics"></a>特征

网络 INF 文件中的每个 *DDInstall* 部分必须具有 **特征** 条目。 **特征**条目指定正在安装的网络组件的某些特征，并可能会限制用户对该组件的操作。 例如，" **特征** " 条目可以指定组件是否支持用户界面、是否可以删除，或者是否对用户隐藏了该组件。

**特征**条目可以具有以下一个或多个值 (将多个值求和) ：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">十六进制值</th>
<th align="left">名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>NCF_VIRTUAL</p></td>
<td align="left"><p>组件是一个虚拟适配器。 设备不在物理总线上，如 PCI 总线或 USB，但位于根总线上。 此标志仅适用于使用 Net 设备安装程序类的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>NCF_SOFTWARE_ENUMERATED</p></td>
<td align="left"><p>组件是一个软件枚举的适配器。 此标志仅适用于使用 Net 设备安装程序类的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>NCF_PHYSICAL</p></td>
<td align="left"><p>组件是一个物理适配器，驱动程序直接与 (例如，通过 PCI 总线) 或通过 USB) 的间接 (进行通信。</p>
<p>如果驱动程序支持物理网络接口，则选择此选项。¹此标志仅适用于使用 Net 设备安装程序类的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>NCF_HIDDEN</p></td>
<td align="left"><p>组件不应在任何用户界面中显示。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NCF_NO_SERVICE</p></td>
<td align="left"><p>组件没有关联的服务 (设备驱动程序) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NCF_NOT_USER_</p>
<p>去除</p></td>
<td align="left"><p>用户不能删除组件 (例如，通过 "控制面板" 或设备管理器) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80</p></td>
<td align="left"><p>NCF_HAS_UI</p></td>
<td align="left"><p>组件支持用户界面 (例如，"高级" 页或自定义属性表) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>NCF_FILTER</p></td>
<td align="left"><p>组件是一个筛选器中间驱动程序。  Windows 10 或更高版本中不支持筛选中间驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>NCF_NDIS_PROTOCOL</p></td>
<td align="left"><p>组件需要绑定引擎提供给 <strong>NetTrans</strong> 设备安装程序类的 unload 事件 (通常由使用 <strong>空间</strong> 设备安装程序类) 的筛选器中间驱动程序使用。</p></td>
</tr>
</tr>
<tr class="even">
<td align="left"><p>0x40000</p></td>
<td align="left"><p>NCF_LW_FILTER</p></td>
<td align="left"><p>组件是轻型筛选器驱动程序。  此标志仅适用于使用空间设备安装程序类的驱动程序。</p></td>
</tr>
</tbody>
</table>

 

¹使用 Windows Server 2012 R2 时，系统上至少有一个网络接口必须标记有 NCF 物理，才能 \_ 获得 DHCPv6 客户端的资格。

不允许使用以下 **特性** 值组合：

-   NCF \_ VIRTUAL、NCF \_ SOFTWARE \_ 和 NCF \_ 物理都是互斥的。 

-   NCF \_ 不 \_ 能将任何服务与 NCF \_ VIRTUAL、NCF \_ SOFTWARE \_ 或 NCF 实物一起使用 \_ 。 虚拟、软件枚举或物理适配器必须始终具有关联的服务 (设备驱动程序) 。

下面是支持用户界面的物理适配器的 **特征** 条目的示例：

```INF
Characteristics = 0x84; NCF_PHYSICAL, NCF_HAS_UI
```

### <a name="bustype"></a>BusType

物理网络适配器的 *DDInstall* 部分必须包含一个 **BusType** 条目，该条目指定可在其上运行适配器的总线 (类型（如 PCI 或 ISA) ）。 **BusType**条目的可能值由 \_ ndis 标头文件中的接口类型枚举指定 () ，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">BusType 项</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ISA</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>EISA</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MicroChannel</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>TurboChannel</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCIBus</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>VMEbus</p></td>
<td align="left"><p>6</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NuBus</p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCMCIABus</p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Cbus</p></td>
<td align="left"><p>9</p></td>
</tr>
<tr class="even">
<td align="left"><p>MPIBus</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MPSABus</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="even">
<td align="left"><p>PNPISABus</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PNPBus</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

**注意**   如果适配器可在多种类型的总线上运行，则安装该适配器的 INF 文件应包含每种总线类型的*DDInstall*部分。

 

例如，如果适配器可在 ISA 总线和 PnPISA 总线上运行，则该适配器的 INF 文件应包含 ISA 的 *DDInstall* 部分和 PnPISA 的 *DDInstall* 部分。 每个此类*DDInstall*部分中的**BusType**条目应为该部分指定相应的总线类型，如下所示：

```INF
[a1.isa]
BusType=1
 
[a1.pnpisa]
BusType=14
```

### <a name="port1devicenumber-and-port1functionnumber"></a>Port1DeviceNumber 和 Port1FunctionNumber

安装多端口网络适配器的 INF 文件的 *DDInstall* 部分必须包含 **Port1DeviceNumber** 项或 **Port1FunctionNumber** 项。 如果指定这样一项，则会在 " **连接属性** " 对话框中显示适配器的端口信息 (通过 " **网络** 和 **拨号连接** " 文件夹访问该对话框，在选择适配器名称或图标时) 。

-   如果适配器的端口号按顺序映射到 PCI 设备号，请使用 **Port1DeviceNumber** 项。 将 **Port1DeviceNumber** 设置为序列中的第一个 PCI 设备号。 例如，如果 PCI 设备号4映射到端口1，PCI 设备号5映射到端口2，PCI 设备号6映射到端口3，依此类推，请使用以下项：
    ```INF
    Port1DeviceNumber = 4
    ```

-   如果适配器的端口号按顺序映射到 PCI 函数号，请使用 **Port1FunctionNumber** 项。 将 **Port1FunctionNumber** 设置为序列中的第一个 PCI 函数号。 例如，如果 PCI 函数号2映射到端口1，PCI 函数编号3映射到端口2，PCI 函数号4映射到端口3，依此类推，请使用以下项：
    ```INF
    Port1FunctionNumber = 2
    ```

**注意**   假定 PCI 设备号或 PCI 函数到端口号的映射为静态。 它还假定适配器的端口按顺序编号。

 

**Port1DeviceNumber**和**Port1FunctionNumber**项是互斥的。 如果给定 *DDInstall* 部分中同时存在这两个条目，则只使用 **Port1DeviceNumber** 条目。

 

