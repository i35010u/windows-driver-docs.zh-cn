---
title: 控制方法输入缓冲区结构
description: 控制方法输入缓冲区结构
ms.assetid: 41d4c53f-9dc7-4723-9707-ae48ff07f5f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f26b93784dd1782bf84d245e683eb9d07ccf6e7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355875"
---
# <a name="control-method-input-buffer-structures"></a>控制方法输入缓冲区结构


ACPI 驱动程序支持[ **IOCTL\_ACPI\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)请求。 设备的驱动程序可以使用此请求来评估是请求发送到设备的 ACPI 命名空间中的直接子对象的控制方法。 IOCTL\_ACPI\_EVAL\_方法请求支持以下输入的结构：

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI\_EVAL\_INPUT\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)  
此结构提供的缓冲区的签名和控制方法不采用一个输入的参数的名称。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_SIMPLE\_INTEGER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)  
此结构提供的结构的签名、 控件的方法的名称和类型为 ULONG 的单个输入的参数值。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)  
此结构提供的结构的签名、 控制方法，以及是以 NULL 结尾的 ASCII 字符串的输入的参数的名称。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_复杂**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)  
此结构提供的结构的签名、 控件的方法的名称和一个输入的数组[ **ACPI\_方法\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)结构。 该数组可以包含七个此类结构的最大数目。 ACPI\_方法\_结构可以包含 ULONG 整数、 ASCII 字符串、 ACPI 包描述或自定义数据的数组的参数。

Windows 还支持[ **IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)请求。 设备的驱动程序可以使用此请求来评估是请求发送到设备的 ACPI 命名空间中的子代的子对象的控制方法。 IOCTL\_ACPI\_EVAL\_方法\_EX 请求支持以下输入的结构：

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)  
此结构提供的结构的路径和名称的一种 control 方法不采用一个输入的参数的签名。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_SIMPLE\_INTEGER\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)  
此结构提供的结构的路径和名称采用单个整数作为输入参数的类型 ULONG64 的控制方法的签名。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)  
此结构提供的结构的路径和名称使用单一的以 NULL 结尾的 ASCII 字符串作为输入参数的控制方法的签名。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_COMPLEX\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)  
此结构提供的结构的路径和名称使用 ACPI 的数组的控制方法的签名\_方法\_参数结构作为输入。 该数组可以包含七个此类结构的最大数目。 ACPI\_方法\_结构可以包含 ULONG 整数、 ASCII 字符串、 ACPI 包描述或自定义数据的数组的参数。

若要获取的路径和名称的设备的 ACPI 命名空间中的子对象，用于设备的驱动程序可以使用[ **IOCTL\_ACPI\_枚举\_子级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求，作为中所述[枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)。
