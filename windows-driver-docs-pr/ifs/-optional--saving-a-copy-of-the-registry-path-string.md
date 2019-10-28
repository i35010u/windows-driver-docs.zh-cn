---
title: 可有可无保存注册表路径字符串的副本
description: 可有可无保存注册表路径字符串的副本
ms.assetid: cf3b8649-6fb0-4ada-816c-5c7783918b2f
keywords:
- RegistryPath 字符串副本
- 保存 RegistryPath 字符串副本
- 复制 RegistryPath 字符串
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 890dfcfa26e341939dad8b60e7796c93264f2762
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841517"
---
# <a name="optional-saving-a-copy-of-the-registry-path-string"></a>\[可选\] 保存注册表路径字符串的副本


## <span id="ddk_saving_a_copy_of_the_registry_path_string_if"></span><span id="DDK_SAVING_A_COPY_OF_THE_REGISTRY_PATH_STRING_IF"></span>


**请注意**   仅当筛选器驱动程序在**DriverEntry**例程返回后需要使用注册表路径时，此步骤才是必需的。

 

保存作为输入传递给**DriverEntry**的*RegistryPath*字符串的副本。 此参数指向一个计数的 Unicode 字符串，该字符串指定驱动程序的注册表项的路径， **\\注册表\\Machine\\System\\CurrentControlSet\\Services\\** <em>DriverName</em>，其中*DriverName*是驱动程序的名称。 如果稍后需要*RegistryPath*字符串，则**DriverEntry**必须保存该字符串的副本，而不只是指向它的指针，因为在**DriverEntry**例程返回后指针不再有效。 可以使用[**RtlCopyUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcopyunicodestring)例程将*RegistryPath*源字符串复制到目标字符串。

 

 




