---
title: 网络 INF 文件中的 DDInstall 节
description: 网络 INF 文件中的 DDInstall 节
ms.assetid: f6621796-0d1f-4d96-9850-720718e7ac44
keywords:
- INF 文件 WDK 网络，DDInstall 部分
- 可使用网络 INF 文件 WDK，DDInstall 部分
- DDInstall 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18810cddf20c9e58bbd9b332e8ea1ef255a8cfc1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354628"
---
# <a name="ddinstall-section-in-a-network-inf-file"></a>网络 INF 文件中的 DDInstall 节





一个*DDInstall*网络 INF 文件中的部分基于泛型[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。

一个*DDInstall*网络 INF 文件中的节具有以下特定于网络的条目：

-   [特征](#characteristics)
-   [BusType](#bustype)
-   [Port1DeviceNumber 和 Port1FunctionNumber](#port1devicenumber-and-port1functionnumber)

### <a name="characteristics"></a>特性

每个*DDInstall*必须具有网络 INF 文件中的节**特征**条目。 **特征**条目指定要安装的网络组件的某些特征，并可能会限制有关该组件的用户的操作。 例如，**特征**条目可以指定该组件是否支持用户界面、 是否可以删除它，或是否从用户隐藏。

**特征**条目可以有一个或多个以下值 （多个值将汇总在一起）：

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>NCF_VIRTUAL</p></td>
<td align="left"><p>组件是虚拟适配器。 设备不在物理总线，如 PCI 总线或 USB、 但根总线上。 此标志才适用于驱动程序使用的网络设备安装程序类。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>NCF_SOFTWARE_ENUMERATED</p></td>
<td align="left"><p>组件是软件枚举适配器。 此标志才适用于驱动程序使用的网络设备安装程序类。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>NCF_PHYSICAL</p></td>
<td align="left"><p>组件是驱动程序与之直接通信 （例如，通过 PCI 总线） 的物理适配器或间接地 （例如，通过 USB）。</p>
<p>选择此选项的驱动程序支持物理网络接口。 ¹ 此标志是否仅适用于驱动程序使用的网络设备安装程序类。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>NCF_HIDDEN</p></td>
<td align="left"><p>组件应不会显示任何用户界面中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NCF_NO_SERVICE</p></td>
<td align="left"><p>组件不具有关联的服务 （设备驱动程序）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NCF_NOT_USER_</p>
<p>可移动</p></td>
<td align="left"><p>组件无法删除用户 （例如，通过控制面板或设备管理器）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80</p></td>
<td align="left"><p>NCF_HAS_UI</p></td>
<td align="left"><p>组件支持的用户界面 （例如，高级页上或自定义属性表）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>NCF_FILTER</p></td>
<td align="left"><p>组件是一个中间筛选器驱动程序。  筛选器中间驱动程序不支持在 Windows 10 或更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>NCF_NDIS_PROTOCOL</p></td>
<td align="left"><p>组件需要由绑定引擎提供卸载事件<strong>NetTrans</strong>设备安装程序类 (通常由筛选器中间的驱动程序使用该对话框<strong>NetService</strong>设备安装程序类）。</p></td>
</tr>
</tr>
<tr class="even">
<td align="left"><p>0x40000</p></td>
<td align="left"><p>NCF_LW_FILTER</p></td>
<td align="left"><p>组件是一个轻型筛选器驱动程序。  此标志才适用于使用 NetService 设备安装程序类的驱动程序。</p></td>
</tr>
</tbody>
</table>

 

¹When 使用 Windows Server 2012 R2，在系统上的至少一个网络接口必须标有 NCF\_物理才有资格享受 DHCPv6 客户端。

以下的组合**特征**不允许值：

-   NCF\_虚拟、 NCF\_软件\_枚举和 NCF\_物理互相排斥。 

-   NCF\_否\_服务不能用于 NCF\_虚拟、 NCF\_软件\_ENUMERATED 或 NCF\_物理。 虚拟的软件枚举，或物理适配器必须始终具有关联的服务 （设备驱动程序）。

以下是一种**特征**支持用户界面的物理适配器的条目：

```INF
Characteristics = 0x84; NCF_PHYSICAL, NCF_HAS_UI
```

### <a name="bustype"></a>BusType

一个*DDInstall*部分的物理网络适配器必须包含**BusType**适配器可以函数指定的类型 （如 PCI 或 ISA） 总线的条目。 可能的值**BusType**由接口指定项\_NDIS 标头文件 (ndis.h) 中，如下所示键入枚举：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">BusType 条目</th>
<th align="left">ReplTest1</th>
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

 

**请注意**  如果适配器可以在多个类型的总线上正常工作，安装该适配器的 INF 文件应包含*DDInstall*部分，了解每个总线类型。

 

例如，如果适配器可以在 ISA 总线和 PnPISA 总线上正常工作，该适配器的 INF 文件应包含*DDInstall*部分，了解 ISA 和一个*DDInstall* PnPISA 的部分。 **BusType**中每个此类条目*DDInstall*部分应指定该部分的相应的总线类型，如下所示：

```INF
[a1.isa]
BusType=1
 
[a1.pnpisa]
BusType=14
```

### <a name="port1devicenumber-and-port1functionnumber"></a>Port1DeviceNumber 和 Port1FunctionNumber

*DDInstall*部分中安装多端口网络适配器的 INF 文件必须包含**Port1DeviceNumber**条目或**Port1FunctionNumber**条目。 指定的这一项会导致适配器的端口信息中显示**连接属性**对话框中 (这通过访问**网络**和**拨号连接**文件夹) 时选择的适配器名称或图标。

-   如果适配器的端口号将按顺序映射到 PCI 设备号，使用**Port1DeviceNumber**条目。 设置**Port1DeviceNumber**与序列中的第一个 PCI 设备数。 例如，如果 PCI 设备号 4 将映射到端口 1，PCI 设备数字 5 映射到端口 2，PCI 设备编号 6 映射到端口 3，依此类推，请使用以下项：
    ```INF
    Port1DeviceNumber = 4
    ```

-   如果适配器的端口号将按顺序映射到 PCI 函数数字，使用**Port1FunctionNumber**条目。 设置**Port1FunctionNumber**序列中的第一个 PCI 函数数字。 例如，如果 PCI 函数号 2 将映射到端口 1，PCI 函数数字 3 映射到端口 2，PCI 函数数字 4 映射到端口 3，依此类推，使用以下项：
    ```INF
    Port1FunctionNumber = 2
    ```

**请注意**  假定 PCI 设备号或端口号为 PCI 函数的映射为静态。 它还假定按顺序编号的适配器的端口。

 

**Port1DeviceNumber**并**Port1FunctionNumber**条目是互相排斥。 如果这两个条目都位于给定*DDInstall*部分中，仅**Port1DeviceNumber**使用项。

 

 





