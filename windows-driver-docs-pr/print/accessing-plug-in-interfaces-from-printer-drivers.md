---
title: 从打印机驱动程序访问插件接口
description: 从打印机驱动程序访问插件接口
ms.assetid: 639734c9-1aac-428c-bd5b-803607f1cf66
keywords:
- COM 接口 WDK 打印，访问插件接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32135bc1d5bffdb01806939580f37c663d934c9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837569"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>从打印机驱动程序访问插件接口





如果安装了 UI 插件或呈现插件，则打印机驱动程序（Unidrv 或 Pscript5）将使用以下调用序列获取对插件的[IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)的访问权限。[IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或[IPrintOemPS2](iprintoemps2-com-interface.md) COM 接口：

1.  驱动程序调用 LoadLibrary 来加载插件 DLL，这将导致调用插件的 `DllMain` 函数。

2.  驱动程序调用插件的 `DllGetClassObject` 函数，该函数返回指向插件的 IClassFactory 接口的指针。

3.  驱动程序调用 IClassFactory 接口的 CreateInstance 方法，并指定**IID\_IUnknown**的接口标识符，这会使方法创建插件[IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)[的实例。IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或[IPrintOemPS2](iprintoemps2-com-interface.md)接口，并返回指向实例的 IUnknown 接口的指针。

4.  驱动程序调用 IUnknown 接口的 QueryInterface 方法，以确定插件支持哪个版本的[IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或[IPrintOemPS2](iprintoemps2-com-interface.md)接口，并接收指向支持的接口的指针。

5.  驱动程序调用插件接口的 `PublishDriverInterface` 方法，使驱动程序的 IPrintOemDriverUI、IPrintCoreUI2、IPrintOemDriverUni、IPrintOemDriverPS 或 IPrintCorePS2 接口可用于插件。

6.  如果插件已经实现了[IPrintOemUni](iprintoemuni-com-interface.md)接口，则驱动程序将调用[**IPrintOemUni：： GetImplementedMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)来确定已实现的接口方法。 同样，如果插件实现了[IPrintOemUni2](iprintoemuni2-com-interface.md)接口，则驱动程序将调用**IPrintOemUni2：： GetImplementedMethod**来实现相同的目的。

 

 




