---
title: 从打印机驱动程序访问插件接口
description: 从打印机驱动程序访问插件接口
ms.assetid: 639734c9-1aac-428c-bd5b-803607f1cf66
keywords:
- COM 接口 WDK 打印，请访问插件接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c04218eb15f8fd938cbeba4a393c07772b4b34c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369006"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>从打印机驱动程序访问插件接口





如果插件或呈现的 UI 插件已安装，打印机驱动程序 （Unidrv 或 Pscript5） 使用以下调用的序列要获得访问权限的即插即用接[IPrintOemUI](iprintoemui-com-interface.md)， [IPrintOemUI2](iprintoemui2-com-interface.md)， [IPrintOemUni](iprintoemuni-com-interface.md)， [IPrintOemUni2](iprintoemuni2-com-interface.md)， [IPrintOemUni3](iprintoemuni3-com-interface.md)， [IPrintOemPS](iprintoemps-com-interface.md)，或[IPrintOemPS2](iprintoemps2-com-interface.md)COM 接口：

1.  该驱动程序调用 LoadLibrary 加载插件 DLL，这会导致的即插即用接调用`DllMain`函数。

2.  该驱动程序调用的即插即用接`DllGetClassObject`函数，它将指针返回到的即插即用接 IClassFactory 接口。

3.  该驱动程序调用 IClassFactory 接口的 CreateInstance 方法，指定的接口标识符**IID\_IUnknown**，这将导致要创建的即插即用的项的实例的方法[IPrintOemUI](iprintoemui-com-interface.md)， [IPrintOemUI2](iprintoemui2-com-interface.md)， [IPrintOemUni](iprintoemuni-com-interface.md)， [IPrintOemUni2](iprintoemuni2-com-interface.md)， [IPrintOemUni3](iprintoemuni3-com-interface.md)， [IPrintOemPS](iprintoemps-com-interface.md)，或[IPrintOemPS2](iprintoemps2-com-interface.md)接口，并返回指向实例的 IUnknown 接口的指针。

4.  该驱动程序调用 IUnknown 接口的 QueryInterface 方法，以确定哪个版本的[IPrintOemUI](iprintoemui-com-interface.md)， [IPrintOemUI2](iprintoemui2-com-interface.md)， [IPrintOemUni](iprintoemuni-com-interface.md)， [IPrintOemUni2](iprintoemuni2-com-interface.md)， [IPrintOemUni3](iprintoemuni3-com-interface.md)， [IPrintOemPS](iprintoemps-com-interface.md)，或者[IPrintOemPS2](iprintoemps2-com-interface.md)插件，并接收支持接口指向受支持的接口指针。

5.  该驱动程序调用插件接口`PublishDriverInterface`方法以使驱动程序的 IPrintOemDriverUI、 IPrintCoreUI2、 IPrintOemDriverUni、 IPrintOemDriverPS 或 IPrintCorePS2 接口可用于该插件。

6.  如果该插件已实现[IPrintOemUni](iprintoemuni-com-interface.md)接口，驱动程序调用[ **IPrintOemUni::GetImplementedMethod** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)来确定的接口方法具有尚未实现。 同样，如果该插件已实现[IPrintOemUni2](iprintoemuni2-com-interface.md)接口，驱动程序调用**IPrintOemUni2::GetImplementedMethod**实现相同目的。

 

 




