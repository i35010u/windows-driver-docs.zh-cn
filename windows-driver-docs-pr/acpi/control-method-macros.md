---
title: 控制方法宏
description: 控制方法宏
ms.assetid: cffcfb7a-c949-4bc9-a92f-349f5637ab84
keywords:
- ACPI 控制方法 WDK，宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b240e0e0a329502d1695950221999adbab4aa19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355858"
---
# <a name="control-method-macros"></a>控制方法宏


驱动程序可以使用以下宏来设置与 ACPI Ioctl 一起使用的输入的参数的[评估控制方法](evaluating-acpi-control-methods.md):

[**ACPI\_方法\_设置\_自变量\_整数**](acpi-method-set-argument-integer.md)

[**ACPI\_方法\_设置\_自变量\_字符串**](acpi-method-set-argument-string.md)

[**ACPI\_方法\_设置\_自变量\_缓冲区**](acpi-method-set-argument-buffer.md)

评估控件方法返回的输出参数中的 ACPI Ioctl**自变量**的成员[ **ACPI\_EVAL\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)结构，其中**自变量**成员是一个数组[ **ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构。 驱动程序可以使用以下宏来帮助处理数组 ACPI\_方法\_参数结构：

[**ACPI\_方法\_自变量\_长度**](acpi-method-argument-length.md)

[**ACPI\_METHOD\_ARGUMENT\_LENGTH\_FROM\_ARGUMENT**](acpi-method-argument-length-from-argument.md)

[**ACPI\_METHOD\_NEXT\_ARGUMENT**](acpi-method-next-argument.md)

[ **IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求检索的路径和名称的请求发送到设备的命名空间中的子对象。 ACPI 驱动程序返回的完整路径和名称的枚举的对象开始的 ACPI 命名空间的根。 中返回的路径和名称的子对象**子级**的成员[ **ACPI\_枚举\_子级\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)结构，其中**子级**成员是一个数组[ **ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_enum_child)结构. 驱动程序可以使用以下宏来帮助处理数组 ACPI\_枚举\_子结构：

[**ACPI\_ENUM\_CHILD\_NEXT**](acpi-enum-child-next.md)

[**ACPI\_ENUM\_CHILD\_LENGTH\_FROM\_CHILD**](acpi-enum-child-length-from-child.md)

 

 




