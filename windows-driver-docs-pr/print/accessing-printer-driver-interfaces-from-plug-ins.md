---
title: 从插件访问打印机驱动程序接口
description: 从插件访问打印机驱动程序接口
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM 接口 WDK 打印，访问打印机驱动程序接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c5b41b82d5a94712996f5cdf74ac88e49b3d3df
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217959"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>从插件访问打印机驱动程序接口





如果插件调用的方法属于驱动程序提供的 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreHelperPS](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)、 [IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口，则它必须从驱动程序获取接口指针，如下所示：

1.  插件必须实现 IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemPS 或 IPrintOemPS2 接口的 PublishDriverInterface 方法。

2.  当驱动程序 (Unidrv 或 Pscript5) 调用插件的 PublishDriverInterface 方法时，它将提供一个指向 IPrintOemDriverUI、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) 实例的 IUnknown 接口的指针。

3.  插件必须使用 IUnknown 接口指针调用 IUnknown：： QueryInterface，并指定表示所需版本的 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) 接口的接口标识符。  (有关详细信息，请参阅 [打印机驱动程序的接口标识符](interface-identifiers-for-printer-drivers.md)。 ) 

4.  如果插件指定了表示驱动程序支持的接口版本的接口标识符，则 QueryInterface 返回指向 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) 接口的指针。 请注意，驱动程序将调用接口的 AddRef 方法，该方法 (Windows SDK) 文档中所述的方法，然后将接口指针返回到该插件。 此插件应该保存此指针，稍后再使用它来调用接口方法。

5.  当不再需要 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) 接口指针时，该插件必须调用接口的 Release 方法， () Windows SDK 文档中所述。

为了使插件能够使用新的 Windows Vista [IPrintCoreHelperPS](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)或[IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)接口，插件需要在其[**IPrintOemUI：： GetInfo**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo)、 [**IPrintOemPS：： GetInfo**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)或[**IPrintOemUni：： GetInfo**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo)方法中添加对**OEMGI \_ GETREQUESTEDHELPERINTERFACES**的支持。

 

