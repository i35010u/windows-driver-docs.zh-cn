---
title: 创建插件
description: 创建插件
ms.assetid: 4e52c855-f2c6-49b5-ac79-96dcac785579
keywords:
- COM 接口 WDK 打印，创建插件
- 插件 WDK 打印创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18a79765275c06b11f48d052131c7bd1dda2beb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544503"
---
# <a name="creating-the-plug-in"></a>创建插件





所有打印机驱动程序插件必须都定义 DllMain、 DllGetClassObject 和 DllCanUnloadNow 函数。 它们还必须实现 IClassFactory COM 接口和一个[IPrintOemUI](iprintoemui-com-interface.md)， [IPrintOemUI2](iprintoemui2-com-interface.md)， [IPrintOemUni](iprintoemuni-com-interface.md)， [IPrintOemUni2](iprintoemuni2-com-interface.md)， [IPrintOemUni3](iprintoemuni3-com-interface.md)， [IPrintOemPS](iprintoemps-com-interface.md)，或[IPrintOemPS2](iprintoemps2-com-interface.md) COM 接口。

当您创建[插件的用户界面](user-interface-plug-ins.md)或[呈现插件](rendering-plug-ins.md)，你应根据你的代码[示例 UI 插件](sample-ui-plug-in.md)或[示例呈现插件](sample-rendering-plug-ins.md)WDK 中提供。

若要创建任一类型的插件，必须执行以下操作：

1.  定义 DllMain 函数 （Windows SDK 文档中所述）。

    这是所有 Win32 Dll 的入口点。

2.  定义和导出 DllGetClassObject 函数 （Windows SDK 文档中所述）。

    打印机驱动程序将调用此函数可获得对插件的实现 IClassFactory 接口 （Windows SDK 文档中所述） 的访问权限。 当驱动程序调用 DllGetClassObject 时，它指定一个以下的类标识符 （prcomoem.h 中定义）：

    CLSID\_OEMUI-UI 插件

    CLSID\_OEMRENDER-呈现插件

    该驱动程序还指定的接口标识符**IID\_IClassFactory**。

    DllGetClassObject 函数必须创建其 IClassFactory 接口的实例，并返回一个指向它，如示例代码中所示。

3.  实现 IClassFactory COM 接口。

    IClassFactory 接口的 CreateInstance 方法应创建一个以下 COM 接口的插件的实现的实例：

    [IPrintOemUI](iprintoemui-com-interface.md)， [IPrintOemUI2](iprintoemui2-com-interface.md)， [IPrintOemUni](iprintoemuni-com-interface.md)， [IPrintOemUni2](iprintoemuni2-com-interface.md)， [IPrintOemUni3](iprintoemuni3-com-interface.md)， [IPrintOemPS](iprintoemps-com-interface.md)，或[IPrintOemPS2](iprintoemps2-com-interface.md)

    CreateInstance 方法的输入之一是一个接口标识符。 该驱动程序使用的接口标识符调用 CreateInstance **IID\_IUnknown**，这意味着 CreateInstance 方法必须返回一个指向所创建的实例 （在 Windows SDK 中所述的 IUnknown 接口文档） 中的示例代码所示。

4.  实现一个 IPrintOemUI、 IPrintOemUI2、 IPrintOemUni、 IPrintOemUni2、 IPrintOemUni3、 IPrintOemPS 或 IPrintOemPS2 COM 接口，包括标准的 IUnknown 接口，如示例代码中所示。

    调用由驱动程序实现的方法首先是 IUnknown 接口的 QueryInterface 方法 （Windows SDK 文档中所述）。 此方法接收之一[接口的打印机驱动程序标识符](interface-identifiers-for-printer-drivers.md)作为输入参数。 该驱动程序调用的方法来确定该插件支持哪个版本的接口和用于接收指向受支持的界面。

5.  定义和导出 DllCanUnloadNow 函数 （Windows SDK 文档中所述）。

    DllCanUnloadNow 函数必须返回 S\_确定如果已发布的插件的实现的 IPrintOemUI、 IPrintOemUI2、 IPrintOemUni、 IPrintOemUni2、 IPrintOemUni3、 IPrintOemPS 或 IPrintOemPS2 COM 接口的所有实例。 S\_确定返回指示向驱动程序，该插件可卸载。

    请注意当打印机驱动程序卸载插件 DLL，则它首先调用插件的 DllCanUnloadNow 函数。 DllCanUnloadNow 返回的值，无论打印机驱动程序然后通过调用 FreeLibrary 函数卸载插件 DLL。 这样做是为了确保插件 DLL 卸载该驱动程序在卸载之前。

    如果插件 DLL 必须保持加载 （例如，创建使用该插件 DLL 的线程时），该线程必须加载 DLL，使用对 LoadLibrary 函数的调用。 当线程完成了 DLL 时，它应调用 FreeLibraryAndExitThread 函数将其卸载。 在一个线程已在其中调用 LoadLibrary，驱动程序的调用 FreeLibrary 只是递减该 DLL 的引用计数，从而防止它正在卸载的情况下。 LoadLibrary 和 FreeLibrary，FreeLibraryAndExitThread 函数是 Windows SDK 文档中所述。

 

 




