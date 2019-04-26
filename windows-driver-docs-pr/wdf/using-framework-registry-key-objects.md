---
title: 使用框架注册表项对象
description: 使用框架注册表项对象
ms.assetid: 2236b4e1-2e17-4e59-b12e-70fff5fd7513
keywords:
- 注册表 WDK KMDF
- 注册表项对象 WDK KMDF
- 基于框架的驱动程序 WDK KMDF、 注册表
- 内核模式驱动程序 WDK KMDF、 注册表
- KMDF WDK 注册表
- 内核模式驱动程序框架 WDK、 注册表
- 密钥 WDK KMDF
- 打开注册表项 WDK KMDF
- 删除注册表键 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c21a9983f14ab9992d7001e1698b50ab677a8bfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327211"
---
# <a name="using-framework-registry-key-objects"></a>使用框架注册表项对象


基于框架的驱动程序使用访问注册表*framework 注册表项对象*。 注册表项对象定义使您的驱动程序来创建、 打开和关闭注册表项; 方法添加和删除注册表值;和读取或写入分配给一个注册表值的数据。

若要打开注册表项，您的驱动程序必须调用[ **WdfRegistryOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff549919)。 如果键不存在，该驱动程序必须调用[ **WdfRegistryCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff549917)，这将创建新密钥并将其打开。

当您的驱动程序打开注册表项时，框架将创建一个注册表项对象，表示打开的密钥并向驱动程序返回的对象的句柄。 该驱动程序必须使用对象句柄来访问密钥、 的项下，存在任何子项和项或其子项下存在的任何值。

若要读取的数据的当前分配给注册表值名称，该驱动程序可以调用以下对象方法之一：

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549920)  
检索当前分配给值名称、 framework 分配的缓冲区，以存储数据和创建 framework 内存对象来表示缓冲区的数据。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](https://msdn.microsoft.com/library/windows/hardware/ff549921)  
检索当前分配给多 string 类型的值名称、 创建每个字符串的 framework 字符串对象并将每个字符串对象添加到对象集合的字符串数据。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff549923)  
检索当前分配给字符串类型值名称并将字符串分配给指定的 framework 字符串对象的字符串数据。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff549927)  
检索当前分配给字符串类型值名称并将字符串复制到指定的字符串数据[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)结构。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](https://msdn.microsoft.com/library/windows/hardware/ff549925)  
检索无符号长的单词 (REG\_DWORD) 当前分配给值名称，并将数据复制到指定位置的数据。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](https://msdn.microsoft.com/library/windows/hardware/ff549928)  
检索当前分配给值名称并将数据复制到驱动程序所提供的缓冲区的数据。

若要将数据写入到注册表值，该驱动程序可以调用以下方法之一。 如果值名称已存在，操作系统更新值的数据。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**WdfRegistryAssignMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549901)  
将分配到注册表中指定的值名称的内存缓冲区中包含的数据。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**WdfRegistryAssignMultiString**](https://msdn.microsoft.com/library/windows/hardware/ff549903)  
将一组字符串分配给在注册表中指定的值名称。 字符串包含在驱动程序提供 framework 字符串对象的集合。

<a href="" id="---------wdfregistryassignstring--------"></a>[**WdfRegistryAssignString**](https://msdn.microsoft.com/library/windows/hardware/ff549906)  
将字符串分配给在注册表中指定的值名称。 该字符串包含在 framework 字符串对象。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff549912)  
将指定的 Unicode 字符串分配给在注册表中指定的值名称。

<a href="" id="---------wdfregistryassignulong--------"></a>[**WdfRegistryAssignULong**](https://msdn.microsoft.com/library/windows/hardware/ff549910)  
将指定的无符号长单词值分配给在注册表中指定的值名称。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**WdfRegistryAssignValue**](https://msdn.microsoft.com/library/windows/hardware/ff549913)  
将驱动程序提供的数据缓冲区的内容分配到注册表中指定的值名称。

若要删除的注册表值，该驱动程序必须调用[ **WdfRegistryRemoveValue**](https://msdn.microsoft.com/library/windows/hardware/ff549932)。 若要删除的密钥，该驱动程序必须调用[ **WdfRegistryRemoveKey**](https://msdn.microsoft.com/library/windows/hardware/ff549930)。

若要获取有关注册表的 WDM 信息，请将驱动程序可以调用[ **WdfRegistryWdmGetHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549935)，它返回 WDM 句柄与 framework 注册表项对象表示的注册表项。

您的驱动程序已完成访问注册表项后，它必须调用[ **WdfRegistryClose** ](https://msdn.microsoft.com/library/windows/hardware/ff549914)或[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)以关闭密钥并删除注册表项对象。

 

 





