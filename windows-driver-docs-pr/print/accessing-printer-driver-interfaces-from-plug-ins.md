---
title: 从插件访问打印机驱动程序接口
description: 从插件访问打印机驱动程序接口
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM 接口 WDK 打印，访问打印机驱动程序接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c84acc734e3e73972eb540a96153282e96f010
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837568"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>从插件访问打印机驱动程序接口





如果插件调用的方法属于驱动程序提供的[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)、 [IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或[IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口时，它必须获取驱动程序的接口指针，如下所示：

1.  插件必须实现 IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemPS 或 IPrintOemPS2 接口的 PublishDriverInterface 方法。

2.  当驱动程序（Unidrv 或 Pscript5）调用插件的 PublishDriverInterface 方法时，它将提供一个指向 IPrintOemDriverUI、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或[IPrintCorePS2](iprintcoreps2-com-interface.md)的指针实例的 IUnknown 接口。

3.  插件必须使用 IUnknown 接口指针调用 IUnknown：： QueryInterface，并指定表示所需版本的[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)[的接口标识符。IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 （有关详细信息，请参阅[打印机驱动程序的接口标识符](interface-identifiers-for-printer-drivers.md)。）

4.  如果插件指定了表示驱动程序支持的接口版本的接口标识符，则 QueryInterface 返回指向[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)的指针， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 请注意，驱动程序将调用接口的 AddRef 方法（在 Windows SDK 文档中进行了描述），然后将接口指针返回到该插件。 此插件应该保存此指针，稍后再使用它来调用接口方法。

5.  当不再需要[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口指针时，该插件必须调用接口的 Release 方法（介绍Windows SDK 文档）。

为了使插件能够使用新的 Windows Vista [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)或[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)接口，插件需要在其[**IPrintOemUI：： GETINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo) [**中添加 OEMGI\_GETREQUESTEDHELPERINTERFACES 的支持。IPrintOemPS：： GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)或[**IPrintOemUni：： GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo)方法。

 

 




