---
title: 控制方法宏
description: 控制方法宏
keywords:
- ACPI 控制方法 WDK，宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d3d836d68e1eaef902104009ed17abe897baab4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785085"
---
# <a name="control-method-macros"></a>控制方法宏


驱动程序可以使用以下宏来设置输入参数，这些参数与 [评估控制方法](evaluating-acpi-control-methods.md)的 ACPI IOCTLs 一起使用：

[**ACPI \_ 方法 \_ 集 \_ 参数 \_ 整数**](acpi-method-set-argument-integer.md)

[**ACPI \_ 方法 \_ 集 \_ 参数 \_ 字符串**](acpi-method-set-argument-string.md)

[**ACPI \_ 方法 \_ 集 \_ 参数 \_ 缓冲区**](acpi-method-set-argument-buffer.md)

评估控制方法的 ACPI IOCTLs 返回 [**acpi \_ EVAL \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)结构的 **参数** 成员中的输出参数，其中 **参数** 成员是一个 [**acpi \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构数组。 驱动程序可以使用以下宏来帮助处理 ACPI \_ 方法参数结构的数组 \_ ：

[**ACPI \_ 方法 \_ 参数 \_ 长度**](acpi-method-argument-length.md)

[**ACPI \_ 方法 \_ 自 \_ \_ 变量的 \_ 长度**](acpi-method-argument-length-from-argument.md)

[**ACPI \_ 方法 \_ NEXT \_ 参数**](acpi-method-next-argument.md)

[**IOCTL \_ ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求检索发送请求的设备的命名空间中的子对象的路径和名称。 ACPI 驱动程序将从 ACPI 命名空间的根开始，返回枚举对象的完整路径和名称。 子对象的路径和名称将在 [**ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)的 **子** 成员中返回，**其中，子成员是** [**acpi \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)结构的数组。 驱动程序可以使用以下宏来帮助处理 ACPI \_ 枚举子结构的数组 \_ ：

[**\_后续 ACPI 枚举 \_ 子项 \_**](acpi-enum-child-next.md)

[**\_子 ACPI 枚举子 \_ \_ 长度 \_ \_**](acpi-enum-child-length-from-child.md)

 

