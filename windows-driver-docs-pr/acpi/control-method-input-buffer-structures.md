---
title: 控制方法输入缓冲区结构
description: 控制方法输入缓冲区结构
ms.assetid: 41d4c53f-9dc7-4723-9707-ae48ff07f5f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ee217a998db52c4bdc6c81c05ca9fc42c1d65e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328842"
---
# <a name="control-method-input-buffer-structures"></a>控制方法输入缓冲区结构


ACPI 驱动程序支持[ **IOCTL\_ACPI\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536148)请求。 设备的驱动程序可以使用此请求来评估是请求发送到设备的 ACPI 命名空间中的直接子对象的控制方法。 IOCTL\_ACPI\_EVAL\_方法请求支持以下输入的结构：

<a href="" id="acpi-eval-input-buffer"></a>[**ACPI\_EVAL\_INPUT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff536115)  
此结构提供的缓冲区的签名和控制方法不采用一个输入的参数的名称。

<a href="" id="acpi-eval-input-buffer-simple-integer"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_SIMPLE\_INTEGER**](https://msdn.microsoft.com/library/windows/hardware/ff536119)  
此结构提供的结构的签名、 控件的方法的名称和类型为 ULONG 的单个输入的参数值。

<a href="" id="acpi-eval-input-buffer-simple-string"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff536121)  
此结构提供的结构的签名、 控制方法，以及是以 NULL 结尾的 ASCII 字符串的输入的参数的名称。

<a href="" id="acpi-eval-input-buffer-complex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_复杂**](https://msdn.microsoft.com/library/windows/hardware/ff536116)  
此结构提供的结构的签名、 控件的方法的名称和一个输入的数组[ **ACPI\_方法\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff536125)结构。 该数组可以包含七个此类结构的最大数目。 ACPI\_方法\_结构可以包含 ULONG 整数、 ASCII 字符串、 ACPI 包描述或自定义数据的数组的参数。

Windows 还支持[ **IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)请求。 设备的驱动程序可以使用此请求来评估是请求发送到设备的 ACPI 命名空间中的子代的子对象的控制方法。 IOCTL\_ACPI\_EVAL\_方法\_EX 请求支持以下输入的结构：

<a href="" id="acpi-eval-input-buffer-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536118)  
此结构提供的结构的路径和名称的一种 control 方法不采用一个输入的参数的签名。

<a href="" id="acpi-eval-input-buffer-simple-integer-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_SIMPLE\_INTEGER\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536120)  
此结构提供的结构的路径和名称采用单个整数作为输入参数的类型 ULONG64 的控制方法的签名。

<a href="" id="acpi-eval-input-buffer-simple-string-ex"></a>[**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536122)  
此结构提供的结构的路径和名称使用单一的以 NULL 结尾的 ASCII 字符串作为输入参数的控制方法的签名。

<a href="" id="acpi-eval-input-buffer-complex-ex"></a>[**ACPI\_EVAL\_INPUT\_BUFFER\_COMPLEX\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536117)  
此结构提供的结构的路径和名称使用 ACPI 的数组的控制方法的签名\_方法\_参数结构作为输入。 该数组可以包含七个此类结构的最大数目。 ACPI\_方法\_结构可以包含 ULONG 整数、 ASCII 字符串、 ACPI 包描述或自定义数据的数组的参数。

若要获取的路径和名称的设备的 ACPI 命名空间中的子对象，用于设备的驱动程序可以使用[ **IOCTL\_ACPI\_枚举\_子级**](https://msdn.microsoft.com/library/windows/hardware/ff536147)请求，作为中所述[枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)。
