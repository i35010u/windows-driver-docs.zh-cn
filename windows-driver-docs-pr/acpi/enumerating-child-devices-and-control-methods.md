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
ms.openlocfilehash: 13e053c5a360d38fd08e03749d361a0696bf1698
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355848"
---
# <a name="enumerating-child-devices-and-control-methods"></a>枚举子设备和控制方法


在 ACPI 名称空间中，一个对象，它设备--例如，名为 ABCD-的设备可以有子对象的子设备的设备或设备支持的控制方法。 任何子对象的父设备是子设备可以反过来，以递归方式使子设备的子对象或控制方法。 例如，以下简化 ACPI 名称空间，在 ACPI 名称空间的根指定由\\和 ABCD 的对象是 ACPI 命名空间的根的直接子的设备。 此外，ABCD 的设备有两个名为 CHL1 的直接子设备，CHL2 和子对象是一种 control 方法名为\_FOO。 此外，子设备 CHL2 具有名为 CHL3 的子设备且设备"CHL3"是一个名为的控制方法的子对象\_FOO。

```syntax
\     root of ACPI namespace
 ABCD            parent device 
    CHL1         child device of ABCD
    CHL2         child device of ABCD
       CHL3      child device of CHL2
          _FOO   control method
 _FOO            control method
```

若要使用[ **IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)或[ **IOCTL\_ACPI\_异步\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)，设备的驱动程序提供的路径和名称在 ACPI 名称空间中的控制方法。 为了获得的路径和名称的设备的设备和子对象，Windows 支持[ **IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求。 在本部分作为示例提供，设备的设备堆栈中的驱动程序的简化 ACPI 命名空间引用 ABCD 可用于此请求执行以下操作：

-   枚举设备 ABCD 和 ABCD。 的直接子设备 例如，请求可用于返回 '\\ABCD，''\\ABCD。CHL1，和\\ABCD。CHL2。

-   以递归方式枚举 ABCD。 的命名空间中的所有设备 例如，请求可用于返回 '\\ABCD，''\\ABCD。CHL1，' '\\ABCD。CHL2，和\\ABCD。CHL2。CHL3。

-   以递归方式枚举 ABCD 的提供的名称的所有子代的子对象。 所提供的名称将用作筛选器，以便只有这些子对象具有相同名称的枚举。 例如，对于提供的名称\_FOO，请求可以用于返回 '\\ABCD。\_FOO 和\\ABCD。CHL2。CHL3。\_FOO。

驱动程序将获取的路径和名称的一种 control 方法后，它可以提供的路径和名称作为输入 IOCTL\_ACPI\_EVAL\_方法\_EX 或 IOCTL\_ACPI\_异步\_EVAL\_方法\_EX，如中所述[评估 ACPI 控件方法以同步方式](evaluating-acpi-control-methods-synchronously.md)。

[ **IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求的输入驱动程序分配可变长度[ **ACPI\_枚举\_子级\_输入\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer)结构，其中包含以下成员：

<a href="" id="signature"></a>**签名**  
签名的输入缓冲区，必须设置为 ACPI\_ENUM\_子级\_输入\_缓冲区\_签名。

<a href="" id="flags"></a>**标志**  
一个标志，用于确定在 ACPI 名称空间的设备的 ACPI 驱动程序枚举中的对象。 ACPI 驱动程序返回的完整路径和名称的枚举的对象开始的 ACPI 命名空间的根。 标志必须设置为以下值之一：

<a href="" id="enum-children-immediate-only"></a>枚举\_子级\_即时\_仅  
枚举设备，并枚举设备的直接子设备。

<a href="" id="enum-children-multilevel"></a>枚举\_子级\_MULTILEVEL  
枚举设备，并以递归方式枚举所有子设备的设备。

<a href="" id="enum-children-multilevel----enum-children-name-is-filter-"></a>枚举\_子级\_MULTILEVEL | |枚举\_子级\_名称\_IS\_筛选器   
按位或的枚举\_个子节点和 ENUM\_子级\_名称\_IS\_筛选器枚举其名称为与提供的相同的设备的子对象**名称**成员。

<a href="" id="namelength"></a>**NameLength**  
ASCII 字符数的**名称**数组包含。

<a href="" id="name"></a>**名称**  
包含的 ACPI 驱动程序使用来限制对具有相同名称的那些对象的子对象的枚举子对象名称的以 NULL 结尾四个字符 ASCII 数组。

IOCTL\_ACPI\_枚举\_子级请求在驱动程序分配长度可变的 ACPI 中返回的路径和名称的子对象\_枚举\_子级\_输出\_缓冲区，其中包含以下成员：

<a href="" id="signature"></a>**签名**  
签名的输出缓冲区，必须设置为 ACPI\_ENUM\_子级\_输出\_缓冲区\_签名。

<a href="" id="numberofchildren"></a>**NumberOfChildren**  
ACPI 类型的元素数\_ENUM\_中的子**子级**数组。

<a href="" id="children"></a>**Children**  
数组的元素的类型 ACPI\_枚举\_子。 **名称**成员的 ACPI\_枚举\_子结构包含的路径和名称的子对象，并且**标志**成员指示子对象是否具有子对象。

如果驱动程序分配输出缓冲区足够大，以返回名称的所有枚举的子，ACPI 驱动程序返回没有子级，名称和设置**状态**成员的 IO\_状态\_块对状态请求\_缓冲区\_溢出。 在此情况下，如果大小，以字节为单位，输出缓冲区的至少**sizeof**(ACPI\_ENUM\_子级\_输出\_缓冲区\_签名)，ACPI 驱动程序还设置**NumberOfChildren**大小，以字节为单位，需要用来检索请求的路径和名称。

有关如何枚举子设备的详细信息，请参阅[发送 IOCTL\_ACPI\_ENUM\_子级请求](sending-an-ioctl-acpi-enum-children-request.md)。
