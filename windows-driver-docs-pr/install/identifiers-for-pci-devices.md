---
title: PCI 设备的标识符
description: PCI 设备的标识符
ms.assetid: 58d52af8-9afd-441f-9ed9-92f9e2775226
keywords:
- 设备标识字符串 WDK、 PCI 设备
- PCI 设备-设备标识字符串 WDK
- 标识符 WDK 设备，PCI 设备
- PCI 设备标识符 WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 05/29/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9188b95ec43959eefd11d4eb80d9ee80d9676ad5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544369"
---
# <a name="identifiers-for-pci-devices"></a>PCI 设备的标识符

> [!IMPORTANT]
> 您可以找到在 PCI 设备在中使用的已知 Id 的列表[PCI ID 存储库](https://pci-ids.ucw.cz/)。 到 Windows，使用上的列表 Id `devcon hwids *`。

以下是一系列[的设备标识字符串](device-identification-strings.md)PCI 总线驱动程序使用来报告硬件 Id 的格式。 当插即用 (PnP) 管理器查询硬件的设备 Id 的驱动程序时，PCI 总线驱动程序将返回以升序一般性的硬件 Id 列表。

```cpp
PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)&SUBSYS_s(4)n(4)

PCI\\VEN_v(4)&DEV_d(4)&REV_r(2)

PCI\\VEN_v(4)&DEV_d(4)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)p(2)

PCI\\VEN_v(4)&DEV_d(4)&CC_c(2)s(2)
```

其中：

-   v(4) 是设备的供应商的四个字符 PCI SIG 分配标识符，术语*设备*，遵循 PCI SIG 使用情况，是指特定 PCI 芯片。

-   d(4) 是四个字符设备供应商定义标识符。

-   s(4) 是四个字符供应商定义的子系统标识符。

-   n(4) 是子系统的供应商的四个字符 PCI SIG 分配标识符。

-   r(2) 是两个字符修订号。

-   c(2) 是配置空间中的两个字符基类代码。

-   s(2) 是两个字符子类代码。

-   p(2) 是编程接口代码。

下面是便携式计算机上的显示适配器的硬件 ID 的示例。 此硬件 ID 的格式是 PCI\\VEN_v(4) DEV_d(4) SUBSYS_s(4)n(4) & REV_r(2)。

    PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000&REV_04

下面是修订信息已被移除上一示例中的显示适配器的硬件 ID。 此硬件 ID 的格式是 PCI\\VEN_<em>v(4)</em>& DEV_<em>d(4)</em>& SUBSYS_*s(4)n(4)。*

    PCI\\VEN_102C&DEV_00E0&SUBSYS_00000000

**请注意**在 Windows 10 中，一些此前现在出现硬件 Id 列表中的 Id 将显示在兼容 Id 列表。

## <a name="reporting-compatible-ids"></a>Reporting 兼容 Id

下面是 PCI 总线驱动程序使用来报告兼容 Id 的设备标识字符串格式的列表。 这些格式的各种提供了大量灵活性来指定兼容的 Id。 PCI 总线驱动程序构造驱动程序可以从设备中获取的信息基于兼容 Id 的列表。 当 PnP 管理器兼容的设备 id 查询驱动程序时，PCI 总线驱动程序返回兼容 Id 列表中按顺序排列的兼容性。

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

-   兼容 ID 中的以下字段的定义是相同的硬件 ID 中使用的相应字段的定义： *v(4)*， *r(2)*， *c(2)*，*s(2)*，并*p(2)*。

-   *d(4)* 在 DEV_*d(4)* 字段是四个字符设备供应商定义标识符。

-   *d(4)* 在 DT_*d(4)* 字段为四个字符设备类型，PCI Express 基本规范中指定。

为便携式计算机上的显示适配器的示例中，任何以下兼容 Id 将匹配该适配器的 INF 文件中的信息：

```cpp
PCI\\VEN_102C&DEV_00E0&REV_04

PCI\\VEN_102C&DEV_00E0

PCI\\VEN_102C&DEV_00E0&REV_04&CC_0300

PCI\\VEN_102C&DEV_00E0&CC_030000

PCI\\VEN_102C&DEV_00E0&CC_0300

PCI\\VEN_102C&CC_030000

PCI\\VEN_102C&CC_0300

PCI\\VEN_102C

PCI\\CC_030000

PCI\\CC_0300
```
 

 





