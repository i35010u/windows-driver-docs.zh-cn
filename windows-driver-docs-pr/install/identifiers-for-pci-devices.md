---
title: PCI 设备的标识符
description: PCI 设备的标识符
keywords:
- 设备标识字符串 WDK，PCI 设备
- 标识字符串 WDK 设备，PCI 设备
- 标识符 WDK 设备，PCI 设备
- PCI 设备标识符 WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 05/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: e728932ebaf38d75167e14e0f1d9e72008da6f47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829919"
---
# <a name="identifiers-for-pci-devices"></a>PCI 设备的标识符

> [!IMPORTANT]
> 你可以在 pci [ID 存储库](https://pci-ids.ucw.cz/)中找到 pci 设备中使用的已知 id 列表。 若要列出 Windows 上的 Id，请使用 `devcon hwids *` 。

下面列出了 PCI bus 驱动程序用来报告硬件 Id 的 [设备标识字符串](device-identification-strings.md) 格式。 当即插即用 (PnP) 管理器查询驱动程序的设备硬件 Id 时，PCI 总线驱动程序会按照更通用性的顺序返回硬件 Id 列表。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)

PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)
```

其中：

-  (4) 是由四个字符组成的 PCI SIG 为设备供应商指定的标识符，其中，术语 " *设备*" （遵循 PCI SIG 使用）指的是特定 pci 芯片。 如 [发布限制](../dashboard/publishing-restrictions.md)中所指定， `0000` 和 `FFFF` 对于此标识符无效。

- d (4) 是设备的由四个字符提供商定义的标识符。

- s (4) 是由四个字符供应商定义的子系统标识符。

- n (4) 是由四个字符组成的 PCI SIG 为子系统供应商指定的标识符。 如 [发布限制](../dashboard/publishing-restrictions.md)中所指定， `0000` 和 `FFFF` 对于此标识符无效。

- r (2) 是两字符的修订号。

- c (2) 是来自配置空间的双字符基类代码。

- s (2) 是两字符子类代码。

- p (2) 是编程接口代码。

## <a name="examples"></a>示例

> [!NOTE]
> 在这些示例中，你将需要替换的占位符子系统值 `00000000` 。 如前所述， `0000` 对于 v (4) 和 n (4) 标识符无效。

下面是便携计算机上显示适配器的硬件 ID 的示例。 此硬件 ID 的格式为 PCI \\ VEN_v (4) # B0 DEV_d (4) # B1 SUBSYS_s (4) n (4) # B2 REV_r (2) ：

`PCI\\VEN_1414&DEV_00E0&SUBSYS_00000000&REV_04`

下面是上一示例中的显示适配器的硬件 ID，其中移除了修订信息。 此硬件 ID 的格式为 PCI \\ VEN_ <em>v (4)</em>&DEV_ <em>d (4)</em>&SUBSYS_ ()  () 4 *。*

`PCI\\VEN_1414&DEV_00E0&SUBSYS_00000000`

>[!NOTE]
>在 Windows 10 中，以前出现在 "硬件 Id" 列表中的一些 Id 现在会显示在兼容 Id 列表中。

## <a name="reporting-compatible-ids"></a>报告兼容 Id

下面列出了 PCI bus 驱动程序用于报告兼容 Id 的设备标识字符串格式。 这两种格式提供了很大的灵活性来指定兼容 Id。 PCI 总线驱动程序基于驱动程序可以从设备获取的信息构造一个兼容 Id 列表。 当 PnP 管理器查询驱动程序的兼容 Id 时，PCI 总线驱动程序将返回兼容 Id 的列表，以降低兼容性的顺序。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&CC_c(2)s(2)

PCI\\VEN_v(4)

PCI\\CC_c(2)s(2)p(2)&DT_d(4) (applies only to a PCI Express device)

PCI\\CC_c(2)s(2)p(2)

PCI\\CC_c(2)s(2)&DT_d(4) (applies only to a PCI Express device)

PCI\\CC_c(2)s(2)\`
```

其中：

- 兼容 ID 中的以下字段的定义与硬件 ID 中使用的相应字段的定义相同： *v (4)*， *r (2)*， *c (2)*， *s (2)*， *p ()*。

- *d (4)* 在 DEV_ *d (4)* 字段是设备的由四个字符供应商定义的标识符。

- *d (4)* 在 DT_ *d (4)* 字段是由四个字符表示的设备类型，如 PCI Express 基准规范中所指定。

对于便携式计算机上显示适配器的示例，以下任何兼容 Id 都将与该适配器的 INF 文件中的信息相匹配：

```cpp
PCI\\VEN_1414&DEV_00E0&REV_04

PCI\\VEN_1414&DEV_00E0

PCI\\VEN_1414&DEV_00E0&REV_04&CC_0300

PCI\\VEN_1414&DEV_00E0&CC_030000

PCI\\VEN_1414&DEV_00E0&CC_0300

PCI\\VEN_1414&CC_030000

PCI\\VEN_1414&CC_0300

PCI\\VEN_1414

PCI\\CC_030000

PCI\\CC_0300
```
