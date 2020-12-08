---
title: 从打印机驱动程序访问插件接口
description: 从打印机驱动程序访问插件接口
keywords:
- COM 接口 WDK 打印，访问插件接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61676b39bb0e16eedd1a3bd12067b982e1a6749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794247"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>从打印机驱动程序访问插件接口





如果安装了 UI 插件或呈现插件，则打印机驱动程序 (Unidrv 或 Pscript5) 使用以下调用序列获取对插件的 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或 [IPrintOemPS2](iprintoemps2-com-interface.md) COM 接口的访问权限：

1.  驱动程序调用 LoadLibrary 来加载插件 DLL，这将导致调用插件的 `DllMain` 函数。

2.  驱动程序调用插件的 `DllGetClassObject` 函数，该函数返回指向插件的 IClassFactory 接口的指针。

3.  驱动程序调用 IClassFactory 接口的 CreateInstance 方法，并指定 **IID \_ IUnknown** 的接口标识符，这会使方法创建插件的 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或 [IPrintOemPS2](iprintoemps2-com-interface.md) 接口的实例，并返回指向该实例的 IUnknown 接口的指针。

4.  驱动程序调用 IUnknown 接口的 QueryInterface 方法，以确定插件支持哪个版本的 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或 [IPrintOemPS2](iprintoemps2-com-interface.md) 接口，并接收指向支持的接口的指针。

5.  驱动程序调用插件接口的 `PublishDriverInterface` 方法，使驱动程序的 IPrintOemDriverUI、IPrintCoreUI2、IPrintOemDriverUni、IPrintOemDriverPS 或 IPrintCorePS2 接口可用于插件。

6.  如果插件已经实现了 [IPrintOemUni](iprintoemuni-com-interface.md) 接口，则驱动程序将调用 [**IPrintOemUni：： GetImplementedMethod**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod) 来确定已实现的接口方法。 同样，如果插件实现了 [IPrintOemUni2](iprintoemuni2-com-interface.md) 接口，则驱动程序将调用 **IPrintOemUni2：： GetImplementedMethod** 来实现相同的目的。

 

