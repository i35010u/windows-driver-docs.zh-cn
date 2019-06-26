---
title: 从插件访问打印机驱动程序接口
description: 从插件访问打印机驱动程序接口
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM 接口 WDK 打印，则访问打印机驱动程序接口
- 插件 WDK 打印，访问接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355a168f9e9b5ad377c31875ff2d5f44d544c1df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385410"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>从插件访问打印机驱动程序接口





如果插件调用的方法的驱动程序提供对属于[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)， [IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口，它必须获取的接口指针从驱动程序，如下所示：

1.  该插件必须实现 IPrintOemUI、 IPrintOemUI2、 IPrintOemUni、 IPrintOemUni2、 IPrintOemPS 或 IPrintOemPS2 接口的 PublishDriverInterface 方法。

2.  驱动程序 （Unidrv 或 Pscript5） 调用的即插即用接 PublishDriverInterface 方法时，它会提供指向 IPrintOemDriverUI [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)实例的 IUnknown 接口。

3.  该插件必须使用 IUnknown 接口指针调用 iunknown:: Queryinterface，指定表示所需的版本的接口标识符[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 (有关详细信息，请参阅[打印机驱动程序的接口标识符](interface-identifiers-for-printer-drivers.md)。)

4.  如果插件指定接口标识符表示驱动程序支持的接口版本，QueryInterface 将返回一个指向[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)接口。 请注意，该驱动程序接口的 AddRef 之前调用方法 （Windows SDK 文档中所述） 它返回到该插件的接口指针。 该插件应该保存此指针以更高版本使用它来调用接口方法。

5.  当[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md)不再需要的接口指针，该插件必须调用接口的释放方法 （Windows SDK 文档中所述）。

为插件以使用新的 Windows Vista [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)或[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)接口，以添加对支持的插件需要**OEMGI\_GETREQUESTEDHELPERINTERFACES**在其[ **IPrintOemUI::GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-getinfo)， [ **IPrintOemPS::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-getinfo)，或[ **IPrintOemUni::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-getinfo)方法。

 

 




