---
title: 发布接口
description: 发布接口
ms.assetid: 3beefaa0-58b9-459a-89e5-1d9d81e80519
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- helper 接口 WDK 打印机接口 DLL
- 发布 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db3a1255d1316b0cba1797fcfebbba49a5d9710
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840416"
---
# <a name="publishing-the-interfaces"></a>发布接口


插件通常通过一种称为 "发布" 的机制接收在核心驱动程序中实现行为的对象的实例。 [IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)、 [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)和[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni) helper 接口通过该相同模型发布，但有一些细微的差异。

以下列表汇总了 Unidrv 和 Pscript5 在用户界面（UI）和呈现模块中发布对象的顺序。 对于这四个模块中的每个模块，列表中的数字指示对象的发布顺序，而名为的 COM 接口指示对象所实现的接口。

在任何给定的模块中，驱动程序应该只保存一个已发布的对象，方法是保存指针并对该对象调用**AddRef**方法。 插件存储对对象的引用后，插件应返回\_"确定"。 核心驱动程序将停止发布接口。 此模型与以前的发布机制截然不同。

在 UI 上下文中，对象被发布到类上的**IPrintOemUI**接口，该类的类标识符是 CLSID\_OEMUI。 在呈现上下文中，将对象发布到**IPrintOemPS**或**IPrintOemUni**接口。

以下列表中用星号（\*）标记的对象将发布到**IPrintOemPrintTicketProvider**接口。

### <a href="" id="unidrv-ui-module-publishing-order"></a>Unidrv UI 模块发布顺序

1.  **IUnknown**和 \***IPrintCoreHelper**和**IPrintCoreHelperUni**

2.  **IUnknown**和**IPrintOemDriverUI**

### <a href="" id="unidrv-render-module-publishing-order"></a>Unidrv 呈现模块发布顺序

1.  **IUnknown**和**IPrintCoreHelper**和**IPrintCoreHelperUni**

2.  **IUnknown**和**IPrintOemDriverUni**

### <a href="" id="pscript5-ui-module-publishing-order"></a>Pscript5 UI 模块发布顺序

1.  **IUnknown**和 \***IPrintCoreHelper**和**IPrintCoreHelperPS**

2.  **IUnknown**和**IPrintCoreUI2**

3.  **IUnknown**和**IPrintOemDriverUI**

### <a href="" id="pscript5-render-module-publishing-order"></a>Pscript5 呈现模块发布顺序

1.  **IUnknown**和**IPrintCoreHelper**和**IPrintCoreHelperPS**

2.  **IUnknown**和**IPrintCorePS2**

 

 




