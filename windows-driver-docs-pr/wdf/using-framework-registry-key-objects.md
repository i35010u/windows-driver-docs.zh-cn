---
title: 使用框架注册表项对象
description: 使用框架注册表项对象
ms.assetid: 2236b4e1-2e17-4e59-b12e-70fff5fd7513
keywords:
- 注册表 WDK KMDF
- 注册表-密钥对象 WDK KMDF
- 基于框架的驱动程序 WDK KMDF，注册表
- 内核模式驱动程序 WDK KMDF、注册表
- KMDF WDK，注册表
- 内核模式驱动程序框架 WDK，注册表
- 密钥 WDK KMDF
- 打开注册表项 WDK KMDF
- 删除注册表项 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77596e443517054aeb83ab19c398ca7cfb2be8f0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187761"
---
# <a name="using-framework-registry-key-objects"></a>使用框架注册表项对象


基于框架的驱动程序使用 *框架注册表项对象*访问注册表。 注册表项对象定义允许您的驱动程序创建、打开和关闭注册表项的方法;添加和删除注册表值;和读取或写入分配给注册表值的数据。

若要打开注册表项，驱动程序必须调用 [**WdfRegistryOpenKey**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryopenkey)。 如果该注册表项不存在，则驱动程序必须调用 [**WdfRegistryCreateKey**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrycreatekey)，这将创建一个新密钥并将其打开。

当驱动程序打开注册表项时，框架会创建一个注册表项对象，该对象表示打开的项并返回驱动程序的对象句柄。 驱动程序必须使用对象句柄来访问该注册表项、该键下存在的任何子项以及该项或其子项下存在的任何值。

若要读取当前分配给注册表值名称的数据，驱动程序可以调用下列对象方法之一：

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)  
检索当前分配给值名称的数据，将数据存储在框架分配的缓冲区中，并创建一个框架内存对象来表示缓冲区。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymultistring)  
检索当前分配给多字符串类型的值名称的字符串数据，创建每个字符串的框架字符串对象，并将每个字符串对象添加到对象集合。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerystring)  
检索当前分配给字符串类型的值名称的字符串数据，并将该字符串分配给指定的框架字符串对象。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryunicodestring)  
检索当前分配给字符串类型的值名称的字符串数据，并将该字符串复制到指定的 [**UNICODE \_ 字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryulong)  
检索当前分配给值名称的无符号长词 (REG \_ DWORD) 数据，并将数据复制到指定位置。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryvalue)  
检索当前分配给值名称的数据，并将数据复制到驱动程序提供的缓冲区。

若要将数据写入注册表值，驱动程序可以调用以下方法之一。 如果值名称已存在，则操作系统会更新值的数据。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**WdfRegistryAssignMemory**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignmemory)  
将内存缓冲区中包含的数据分配到注册表中的指定值名称。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**WdfRegistryAssignMultiString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignmultistring)  
在注册表中将一组字符串分配给指定的值名称。 字符串包含在驱动程序提供的框架字符串对象的集合中。

<a href="" id="---------wdfregistryassignstring--------"></a>[**WdfRegistryAssignString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignstring)  
在注册表中将字符串分配给指定的值名称。 在框架字符串对象中包含该字符串。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignunicodestring)  
在注册表中将指定的 Unicode 字符串分配给指定的值名称。

<a href="" id="---------wdfregistryassignulong--------"></a>[**WdfRegistryAssignULong**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignulong)  
在注册表中将指定的无符号长字值分配给指定的值名称。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**WdfRegistryAssignValue**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignvalue)  
将驱动程序提供的数据缓冲区的内容分配到注册表中指定的值名称。

若要删除注册表值，驱动程序必须调用 [**WdfRegistryRemoveValue**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryremovevalue)。 若要删除某个密钥，驱动程序必须调用 [**WdfRegistryRemoveKey**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryremovekey)。

若要获取有关注册表的 WDM 信息，驱动程序可以调用 [**WdfRegistryWdmGetHandle**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)，这会将一个 WDM 句柄返回到框架注册表项对象表示的注册表项。

驱动程序访问完注册表项后，必须调用 [**WdfRegistryClose**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryclose) 或 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 来关闭该项并删除注册表项对象。

 

