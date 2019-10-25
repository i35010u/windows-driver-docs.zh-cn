---
title: 枚举子设备和控制方法
description: 枚举子设备和控制方法
ms.assetid: fe0553df-a5b9-46c4-8e1d-8b89a7d4ad67
keywords:
- ACPI 设备 WDK，枚举子设备
- ACPI 设备 WDK，枚举控制方法
- ACPI 命名空间 WDK
- ACPI 控制方法 WDK，枚举
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e9300f06b07c88f88f5c6ced9c2765c9ee1b8bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826123"
---
# <a name="enumerating-child-devices-and-control-methods"></a>枚举子设备和控制方法


在 ACPI 命名空间中，作为设备的对象（例如，名为 "ABCD" 的设备），子对象可以是设备的子设备，也可以是设备支持的控制方法。 作为父设备的子设备的任何子对象反过来会以递归方式具有子对象，这些子对象是子设备或控制方法。 例如，在以下简化的 ACPI 命名空间中，ACPI 命名空间的根由 "\\" 指定，对象 "ABCD" 是 ACPI 命名空间的根的直接子项的设备。 此外，设备 "ABCD" 具有两个名为 "CHL1" 和 "CHL2" 的直接子设备，以及一个名为 "\_FOO" 的控制方法的子对象。 此外，子设备 "CHL2" 有一个名为 "CHL3" 的子设备，并且设备 "CHL3" 具有一个子对象，该对象是名为 "\_FOO" 的控制方法。

```syntax
\     root of ACPI namespace
 ABCD            parent device 
    CHL1         child device of ABCD
    CHL2         child device of ABCD
       CHL3      child device of CHL2
          _FOO   control method
 _FOO            control method
```

若要使用[**IOCTL\_acpi\_EVAL\_方法\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)或[**IOCTL\_acpi\_异步\_EVAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)\_\_例如，设备的驱动程序提供了控制方法的路径和名称在 ACPI 命名空间中。 为了帮助获取设备的路径和名称以及设备的子对象，Windows 支持[ **\_ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求的 IOCTL。 引用此部分中提供的简化 ACPI 命名空间作为示例，设备 "ABCD" 的设备堆栈中的驱动程序可以使用此请求执行以下操作：

-   枚举设备 "ABCD" 和 "ABCD" 的直接子设备。 例如，可使用请求来返回 "\\ABCD"\\ABCD。CHL1、' 和 '\\ABCD。CHL2.'

-   以递归方式枚举 "ABCD" 的命名空间中的所有设备。 例如，可使用请求来返回 "\\ABCD"\\ABCD。CHL1\\ABCD。CHL2、' 和 '\\ABCD。CHL2.CHL3.'

-   以递归方式枚举提供的名称的 "ABCD" 的所有子代子对象。 提供的名称用作筛选器，因此仅枚举同名的子对象。 例如，对于所提供的名称 "\_FOO"，该请求可用于返回 "\\ABCD。\_FOO "和"\\ABCD。CHL2.CHL3.\_FOO. "

驱动程序获取控制方法的路径和名称后，它可以提供路径和名称作为 IOCTL\_ACPI\_EVAL\_方法\_EX 或 IOCTL\_ACPI\_ASYNC\_EVAL\_方法\_EX，如[同步计算 ACPI 控制方法](evaluating-acpi-control-methods-synchronously.md)中所述。

[**IOCTL\_ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求会将驱动程序分配的可变长度[**ACPI\_枚举\_子项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer)作为输入\_包含以下成员\_缓冲结构：

<a href="" id="signature"></a>**信号**  
输入缓冲区的签名，必须将其设置为 ACPI\_枚举\_子\_输入\_缓冲区\_签名。

<a href="" id="flags"></a>**随意**  
确定 ACPI 驱动程序要枚举的设备的 ACPI 命名空间中的哪些对象的标志。 ACPI 驱动程序将从 ACPI 命名空间的根开始，返回枚举对象的完整路径和名称。 标志必须设置为以下值之一：

<a href="" id="enum-children-immediate-only"></a>枚举\_子级仅\_立即\_  
枚举设备，并枚举设备的直接子设备。

<a href="" id="enum-children-multilevel"></a>枚举\_子\_多级  
枚举设备，并以递归方式枚举设备的所有子设备。

<a href="" id="enum-children-multilevel----enum-children-name-is-filter-"></a>枚举\_子\_多级 | |枚举\_\_\_筛选器\_名称   
枚举的按位 "或"\_子级和枚举\_子级\_名称\_为\_筛选器枚举其名称与**name**成员提供的名称相同的子对象。

<a href="" id="namelength"></a>**NameLength**  
**名称**数组包含的 ASCII 字符数。

<a href="" id="name"></a>**路径名**  
以 NULL 结尾的四字符 ASCII 数组，其中包含 ACPI 驱动程序用于将子对象的枚举限制为具有相同名称的对象的子对象的名称。

IOCTL\_ACPI\_ENUM\_子请求返回驱动程序分配的可变长度 ACPI\_枚举\_子对象中子对象的路径和名称，\_输出包含以下成员\_缓冲区:

<a href="" id="signature"></a>**信号**  
输出缓冲区的签名，必须将其设置为 ACPI\_枚举\_子\_输出\_缓冲区\_签名。

<a href="" id="numberofchildren"></a>**NumberOfChildren**  
**子**数组中 ACPI\_枚举\_子类型的元素的数目。

<a href="" id="children"></a>**观看**  
ACPI\_子类型的元素的数组\_枚举。 ACPI\_枚举\_子结构的**名称**成员包含子对象的路径和名称，**标志**成员指示子对象是否具有子对象。

如果驱动程序分配的输出缓冲区不够大，无法返回所有枚举的子名称，ACPI 驱动程序将不返回任何子名称，并将请求的 IO\_状态\_块的**状态**成员设置\_缓冲区\_溢出。 在这种情况下，如果输出缓冲区的大小（以字节为单位）至少为**sizeof**（ACPI\_枚举\_子\_输出\_缓冲区\_签名），ACPI 驱动程序还会将**NumberOfChildren**设置为大小检索请求的路径和名称所需的（以字节为单位）。

有关如何枚举子设备的详细信息，请参阅[\_子请求发送 IOCTL\_ACPI\_ENUM](sending-an-ioctl-acpi-enum-children-request.md)。
