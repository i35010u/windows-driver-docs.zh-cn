---
title: 从插件访问打印机驱动程序接口
description: 从插件访问打印机驱动程序接口
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM 接口 WDK 打印，则访问打印机驱动程序接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fd903fec5c4e4c8d8f5e90686adaac7e9152b64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381194"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>从插件访问打印机驱动程序接口





如果插件调用的方法的驱动程序提供对属于[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)， [IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口，它必须获取的接口指针从驱动程序，如下所示：

1.  该插件必须实现 IPrintOemUI、 IPrintOemUI2、 IPrintOemUni、 IPrintOemUni2、 IPrintOemPS 或 IPrintOemPS2 接口的 PublishDriverInterface 方法。

2.  驱动程序 （Unidrv 或 Pscript5） 调用的即插即用接 PublishDriverInterface 方法时，它会提供指向 IPrintOemDriverUI [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)实例的 IUnknown 接口。

3.  该插件必须使用 IUnknown 接口指针调用 iunknown:: Queryinterface，指定表示所需的版本的接口标识符[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 (有关详细信息，请参阅[打印机驱动程序的接口标识符](interface-identifiers-for-printer-drivers.md)。)

4.  如果插件指定接口标识符表示驱动程序支持的接口版本，QueryInterface 将返回一个指向[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 请注意，该驱动程序接口的 AddRef 之前调用方法 （Windows SDK 文档中所述） 它返回到该插件的接口指针。 该插件应该保存此指针以更高版本使用它来调用接口方法。

5.  当[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)不再需要的接口指针，该插件必须调用接口的释放方法 （Windows SDK 文档中所述）。

为插件以使用新的 Windows Vista [IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)或[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)接口，以添加对支持的插件需要**OEMGI\_GETREQUESTEDHELPERINTERFACES**在其[ **IPrintOemUI::GetInfo**](https://msdn.microsoft.com/library/windows/hardware/ff554178)， [ **IPrintOemPS::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553221)，或[ **IPrintOemUni::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff554256)方法。

 

 




