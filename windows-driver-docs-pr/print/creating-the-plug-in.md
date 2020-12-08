---
title: 创建插件
description: 创建插件
keywords:
- COM 接口 WDK 打印，创建插件
- 插件 WDK 打印，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0af16e22a6f76619f526133f0d3d9986b6fc214b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797451"
---
# <a name="creating-the-plug-in"></a>创建插件





所有打印机驱动程序插件必须定义 DllMain、DllGetClassObject 和 DllCanUnloadNow 函数。 它们还必须实现 IClassFactory COM 接口和 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或 [IPrintOemPS2](iprintoemps2-com-interface.md) com 接口。

当你创建 [用户界面插件](user-interface-plug-ins.md) 或 [呈现插件](rendering-plug-ins.md)时，你应该将代码基于 [示例 UI 插件](sample-ui-plug-in.md) 或在 WDK 中提供的 [示例呈现插件](sample-rendering-plug-ins.md) 。

若要创建任一类型的插件，必须执行以下操作：

1.  定义 (Windows SDK 文档) 中所述的 DllMain 函数。

    这是所有 Win32 Dll 的入口点。

2.  定义和导出 Windows SDK 文档)  (所述的 DllGetClassObject 函数。

    打印机驱动程序调用此函数以获取对插件的 IClassFactory 接口实现的访问， (在 Windows SDK 文档) 中介绍。 当驱动程序调用 DllGetClassObject 时，它将指定以下类标识符之一 (在 prcomoem) 中定义：

    CLSID \_ OEMUI-适用于 UI 插件

    CLSID \_ OEMRENDER-用于呈现插件

    驱动程序还指定了 **IID \_ IClassFactory** 的接口标识符。

    DllGetClassObject 函数必须创建其 IClassFactory 接口的实例，并返回指向它的指针，如示例代码所示。

3.  实现 IClassFactory COM 接口。

    IClassFactory 接口的 CreateInstance 方法应创建插件实现的下列 COM 接口之一的实例：

    [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)或 [IPrintOemPS2](iprintoemps2-com-interface.md)

    CreateInstance 方法的输入之一是接口标识符。 驱动程序使用 **IID \_ IUnknown** 的接口标识符调用 CreateInstance，这意味着，createinstance 方法必须返回指向已创建实例的 IUnknown 接口的指针， (如示例代码) Windows SDK 所示。

4.  实现 IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemUni3、IPrintOemPS 或 IPrintOemPS2 COM 接口中的一个，如示例代码所示。

    驱动程序调用的第一种实现方法是 IUnknown 接口的 QueryInterface 方法 (在 Windows SDK 文档) 中进行了介绍。 此方法接收 [打印机驱动程序的接口标识符](interface-identifiers-for-printer-drivers.md) 之一作为输入参数。 驱动程序调用方法来确定插件支持哪个版本的接口，并接收指向支持的接口的指针。

5.  定义和导出 Windows SDK 文档)  (所述的 DllCanUnloadNow 函数。

    \_如果插件实现的 IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemUni3、IPrintOemPS 或 IPRINTOEMPS2 COM 接口的所有实例都已释放，则 DllCanUnloadNow 函数必须返回 "OK"。 S \_ OK 返回向驱动程序指示插件可以卸载。

    请注意，当打印机驱动程序卸载插件 DLL 时，它首先调用插件的 DllCanUnloadNow 函数。 无论 DllCanUnloadNow 返回的值是什么，打印机驱动程序都可以通过调用 FreeLibrary 函数来卸载插件 DLL。 这样做是为了确保在卸载驱动程序之前卸载插件 DLL。

    如果插件 DLL 必须保持加载 (例如，当它创建使用插件 DLL) 的线程时，该线程必须使用对 LoadLibrary 函数的调用来加载 DLL。 当线程完成 DLL 时，应调用 FreeLibraryAndExitThread 函数以将其卸载。 在线程调用 LoadLibrary 的情况下，驱动程序对 FreeLibrary 的调用只是减少 DLL 的引用计数，从而防止其被卸载。 Windows SDK 文档中介绍了 LoadLibrary、FreeLibrary 和 FreeLibraryAndExitThread 函数。

 

 




