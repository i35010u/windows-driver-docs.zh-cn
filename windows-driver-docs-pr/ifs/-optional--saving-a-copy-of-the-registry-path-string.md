---
title: '[可选]正在保存注册表路径字符串的副本'
description: '[可选]正在保存注册表路径字符串的副本'
ms.assetid: cf3b8649-6fb0-4ada-816c-5c7783918b2f
keywords:
- RegistryPath 字符串副本
- 保存 RegistryPath 字符串副本
- 复制 RegistryPath 字符串
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd0bac911f9fd2e9a8fc1fcc8dc387c9f4c5ad7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366795"
---
# <a name="optional-saving-a-copy-of-the-registry-path-string"></a>\[可选\]保存注册表路径字符串的副本


## <span id="ddk_saving_a_copy_of_the_registry_path_string_if"></span><span id="DDK_SAVING_A_COPY_OF_THE_REGISTRY_PATH_STRING_IF"></span>


**请注意**  此步骤是必需的筛选器驱动程序需要使用注册表路径后的，才**DriverEntry**例程返回。

 

保存一份*RegistryPath*字符串作为输入传递**DriverEntry**。 此参数指向一个计数的 Unicode 字符串，指定驱动程序的注册表项的路径**\\注册表\\机\\系统\\CurrentControlSet\\Services\\** <em>DriverName</em>，其中*DriverName*是驱动程序的名称。 如果*RegistryPath*更高版本，将需要字符串**DriverEntry**必须保存一份它，而不仅仅是一个指针指向它，因为指针将不再有效后**DriverEntry**例程返回。 可以使用[ **RtlCopyUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561817)例程，以复制*RegistryPath*源到目标字符串的字符串。

 

 




