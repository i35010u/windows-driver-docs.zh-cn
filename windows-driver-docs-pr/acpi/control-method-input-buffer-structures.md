---
title: 控制方法输入缓冲区结构
description: 控制方法输入缓冲区结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca50ad1c39038149f58d3c853dd36342a050bc22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789501"
---
# <a name="control-method-input-buffer-structures"></a>控制方法输入缓冲区结构


ACPI 驱动程序支持 [**IOCTL \_ ACPI \_ EVAL \_ 方法**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method) 请求。 设备的驱动程序可以使用此请求来计算控制方法，该方法是请求发送到的设备的 ACPI 命名空间中的直接子对象。 IOCTL \_ ACPI \_ EVAL \_ 方法请求支持以下输入结构：

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)  
此结构提供缓冲区的签名和不采用输入参数的控件方法的名称。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 整数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)  
此结构提供结构的签名、控件方法的名称，以及 ULONG 类型的单个输入参数值。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 字符串**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)  
此结构提供结构的签名、控件方法的名称，以及一个以 NULL 结尾的 ASCII 字符串的输入参数。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 复杂**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)  
此结构提供结构的签名、控件方法的名称，以及 [**ACPI \_ 方法 \_ 参数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1) 结构的输入数组。 数组最多可包含七个此类结构。 ACPI \_ 方法 \_ 参数结构可以包含 ULONG 整数、ASCII 字符串、ACPI 包说明或自定义数据的数组。

Windows 还支持 [**IOCTL \_ ACPI \_ EVAL 方法（ \_ \_ 例如**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex) 请求）。 设备的驱动程序可以使用此请求来计算控制方法，该方法是要向其发送请求的设备的 ACPI 命名空间中的后代子对象。 IOCTL \_ ACPI \_ EVAL \_ 方法 \_ EX 请求支持以下输入结构：

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区， \_ 例如**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)  
此结构提供结构的签名，以及不采用输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 整数 \_ EX**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)  
此结构提供结构的签名，以及采用类型为 ULONG64 的单个整数作为输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 字符串（ \_ 例如**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)  
此结构提供结构的签名，以及采用单个以 NULL 结尾的 ASCII 字符串作为输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 复杂 \_ EX**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)  
此结构提供了结构的签名，以及使用 ACPI \_ 方法 \_ 参数结构数组作为输入的控件方法的路径和名称。 数组最多可包含七个此类结构。 ACPI \_ 方法 \_ 参数结构可以包含 ULONG 整数、ASCII 字符串、ACPI 包说明或自定义数据的数组。

若要在设备的 ACPI 命名空间中获取子对象的路径和名称，设备的驱动程序可以使用 [**IOCTL \_ ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children) 请求，如 [枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)中所述。
