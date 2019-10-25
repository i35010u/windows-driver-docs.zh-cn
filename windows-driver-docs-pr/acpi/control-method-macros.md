---
title: 控制方法宏
description: 控制方法宏
ms.assetid: cffcfb7a-c949-4bc9-a92f-349f5637ab84
keywords:
- ACPI 控制方法 WDK，宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052e45c47d3af60e1e7fc9737bec3c3a65c60638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824717"
---
# <a name="control-method-macros"></a>控制方法宏


驱动程序可以使用以下宏来设置输入参数，这些参数与[评估控制方法](evaluating-acpi-control-methods.md)的 ACPI IOCTLs 一起使用：

[**ACPI\_方法\_集\_参数\_整数**](acpi-method-set-argument-integer.md)

[**ACPI\_方法\_集\_参数\_字符串**](acpi-method-set-argument-string.md)

[**ACPI\_方法\_设置\_参数\_缓冲区**](acpi-method-set-argument-buffer.md)

评估控制方法的 ACPI IOCTLs 会将[**acpi\_EVAL\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)的**参数**成员中的输出参数返回\_缓冲结构，其中**参数**成员是一个[**ACPI\_方法的数组\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构。 驱动程序可以使用以下宏来帮助处理 ACPI\_方法\_参数结构的数组：

[**ACPI\_方法\_参数\_长度**](acpi-method-argument-length.md)

[**ACPI\_方法\_参数\_长度\_从\_参数**](acpi-method-argument-length-from-argument.md)

[**ACPI\_方法\_下一个\_参数**](acpi-method-next-argument.md)

[**IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求检索发送请求的设备的命名空间中的子对象的路径和名称。 ACPI 驱动程序将从 ACPI 命名空间的根开始，返回枚举对象的完整路径和名称。 子对象的路径和名称将在[**ACPI\_枚举\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)成员的**子成员中**返回\_输出\_缓冲区结构，其中，**子**成员是[**ACPI\_枚举的数组\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)结构。 驱动程序可以使用以下宏来帮助处理 ACPI\_枚举\_子结构的数组：

[**ACPI\_枚举\_子\_下一步**](acpi-enum-child-next.md)

[**ACPI\_枚举\_子\_长度\_从\_子级**](acpi-enum-child-length-from-child.md)

 

 




