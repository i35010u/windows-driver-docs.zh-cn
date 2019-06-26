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
ms.openlocfilehash: 948145d0768ac32ab1e3f02252abe1ac1612e20e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372253"
---
# <a name="using-framework-registry-key-objects"></a>使用框架注册表项对象


基于框架的驱动程序使用访问注册表*framework 注册表项对象*。 注册表项对象定义使您的驱动程序来创建、 打开和关闭注册表项; 方法添加和删除注册表值;和读取或写入分配给一个注册表值的数据。

若要打开注册表项，您的驱动程序必须调用[ **WdfRegistryOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryopenkey)。 如果键不存在，该驱动程序必须调用[ **WdfRegistryCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrycreatekey)，这将创建新密钥并将其打开。

当您的驱动程序打开注册表项时，框架将创建一个注册表项对象，表示打开的密钥并向驱动程序返回的对象的句柄。 该驱动程序必须使用对象句柄来访问密钥、 的项下，存在任何子项和项或其子项下存在的任何值。

若要读取的数据的当前分配给注册表值名称，该驱动程序可以调用以下对象方法之一：

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)  
检索当前分配给值名称、 framework 分配的缓冲区，以存储数据和创建 framework 内存对象来表示缓冲区的数据。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerymultistring)  
检索当前分配给多 string 类型的值名称、 创建每个字符串的 framework 字符串对象并将每个字符串对象添加到对象集合的字符串数据。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerystring)  
检索当前分配给字符串类型值名称并将字符串分配给指定的 framework 字符串对象的字符串数据。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryunicodestring)  
检索当前分配给字符串类型值名称并将字符串复制到指定的字符串数据[ **UNICODE\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)结构。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryulong)  
检索无符号长的单词 (REG\_DWORD) 当前分配给值名称，并将数据复制到指定位置的数据。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryvalue)  
检索当前分配给值名称并将数据复制到驱动程序所提供的缓冲区的数据。

若要将数据写入到注册表值，该驱动程序可以调用以下方法之一。 如果值名称已存在，操作系统更新值的数据。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**WdfRegistryAssignMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignmemory)  
将分配到注册表中指定的值名称的内存缓冲区中包含的数据。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**WdfRegistryAssignMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignmultistring)  
将一组字符串分配给在注册表中指定的值名称。 字符串包含在驱动程序提供 framework 字符串对象的集合。

<a href="" id="---------wdfregistryassignstring--------"></a>[**WdfRegistryAssignString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignstring)  
将字符串分配给在注册表中指定的值名称。 该字符串包含在 framework 字符串对象。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignunicodestring)  
将指定的 Unicode 字符串分配给在注册表中指定的值名称。

<a href="" id="---------wdfregistryassignulong--------"></a>[**WdfRegistryAssignULong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignulong)  
将指定的无符号长单词值分配给在注册表中指定的值名称。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**WdfRegistryAssignValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignvalue)  
将驱动程序提供的数据缓冲区的内容分配到注册表中指定的值名称。

若要删除的注册表值，该驱动程序必须调用[ **WdfRegistryRemoveValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryremovevalue)。 若要删除的密钥，该驱动程序必须调用[ **WdfRegistryRemoveKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryremovekey)。

若要获取有关注册表的 WDM 信息，请将驱动程序可以调用[ **WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)，它返回 WDM 句柄与 framework 注册表项对象表示的注册表项。

您的驱动程序已完成访问注册表项后，它必须调用[ **WdfRegistryClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryclose)或[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)以关闭密钥并删除注册表项对象。

 

 





