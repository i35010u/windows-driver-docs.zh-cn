---
title: 发布接口
description: 发布接口
ms.assetid: 3beefaa0-58b9-459a-89e5-1d9d81e80519
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- 帮助器接口 WDK 打印机接口 DLL
- 发布 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d8f912fe965419dee97f696558dafa0cb296dbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568858"
---
# <a name="publishing-the-interfaces"></a>发布接口


插件通常接收的一种称为发布机制的核心驱动程序中实现行为的对象的实例。 [IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)， [IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)，并[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)帮助程序接口均通过该同一模型中，有几个不同之处。

以下列表总结了在用户界面 (UI) 中发布和呈现的模块，用来 Unidrv 和 Pscript5 对象的顺序。 对于每个四个模块，在列表中的数字表示在其中发布对象，和名为的 COM 接口指示该对象实现的接口的顺序。

在任何给定的模块，该驱动程序应该保留通过保存一个指针，并调用已发布的对象之一**AddRef**对该对象的方法。 该插件将存储对对象的引用后，该插件应返回 S\_确定。 核心驱动程序将不会再发布接口。 此模型不是明显不同于以前的发布机制。

在用户界面上下文中，将对象发布到**IPrintOemUI**上其类标识符是 CLSID 的类接口\_OEMUI。 在呈现器上下文中，将对象发布到**IPrintOemPS**或**IPrintOemUni**接口。

标有星号的对象 (\*) 在以下列表中将发布到**IPrintOemPrintTicketProvider**接口。

### <a href="" id="unidrv-ui-module-publishing-order"></a> 发布顺序 Unidrv UI 模块

1.  **IUnknown**并\* **IPrintCoreHelper**和**IPrintCoreHelperUni**

2.  **IUnknown**和**IPrintOemDriverUI**

### <a href="" id="unidrv-render-module-publishing-order"></a> 发布顺序 Unidrv 呈现器模块

1.  **IUnknown**并**IPrintCoreHelper**和**IPrintCoreHelperUni**

2.  **IUnknown**和**IPrintOemDriverUni**

### <a href="" id="pscript5-ui-module-publishing-order"></a> 发布顺序 Pscript5 UI 模块

1.  **IUnknown**并\* **IPrintCoreHelper**和**IPrintCoreHelperPS**

2.  **IUnknown**和**IPrintCoreUI2**

3.  **IUnknown**和**IPrintOemDriverUI**

### <a href="" id="pscript5-render-module-publishing-order"></a> 发布顺序 Pscript5 呈现器模块

1.  **IUnknown**并**IPrintCoreHelper**和**IPrintCoreHelperPS**

2.  **IUnknown**和**IPrintCorePS2**

 

 




