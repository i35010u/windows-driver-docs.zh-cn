---
title: 控制方法输入缓冲区结构
description: 控制方法输入缓冲区结构
ms.assetid: 41d4c53f-9dc7-4723-9707-ae48ff07f5f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a75c4386096b2bf34dd048e3c9322345912a608
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824271"
---
# <a name="control-method-input-buffer-structures"></a>控制方法输入缓冲区结构


ACPI 驱动程序支持[**IOCTL\_ACPI\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)请求。 设备的驱动程序可以使用此请求来计算控制方法，该方法是请求发送到的设备的 ACPI 命名空间中的直接子对象。 IOCTL\_ACPI\_EVAL\_方法请求支持以下输入结构：

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI\_EVAL\_输入\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)  
此结构提供缓冲区的签名和不采用输入参数的控件方法的名称。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)  
此结构提供结构的签名、控件方法的名称，以及 ULONG 类型的单个输入参数值。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)  
此结构提供结构的签名、控件方法的名称，以及一个以 NULL 结尾的 ASCII 字符串的输入参数。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_复杂**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)  
此结构提供结构的签名、控件方法的名称，以及[**ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构的输入数组。 数组最多可包含七个此类结构。 ACPI\_方法\_参数结构可以包含 ULONG 整数、ASCII 字符串、ACPI 包说明或自定义数据的数组。

Windows 还支持[ **\_ACPI\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)请求的 IOCTL。 设备的驱动程序可以使用此请求来计算控制方法，该方法是要向其发送请求的设备的 ACPI 命名空间中的后代子对象。 IOCTL\_ACPI\_EVAL\_方法\_EX 请求支持以下输入结构：

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)  
此结构提供结构的签名，以及不采用输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数\_例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)  
此结构提供结构的签名，以及采用类型为 ULONG64 的单个整数作为输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)  
此结构提供结构的签名，以及采用单个以 NULL 结尾的 ASCII 字符串作为输入参数的控件方法的路径和名称。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_复杂的\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)  
此结构提供了结构的签名，以及采用 ACPI\_\_方法数组作为输入的控件方法的路径和名称。 数组最多可包含七个此类结构。 ACPI\_方法\_参数结构可以包含 ULONG 整数、ASCII 字符串、ACPI 包说明或自定义数据的数组。

若要在设备的 ACPI 命名空间中获取子对象的路径和名称，设备的驱动程序可以使用[**IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求，如[枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)中所述。
