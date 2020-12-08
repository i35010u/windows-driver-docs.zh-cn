---
title: 框架基对象
description: 框架基对象
keywords:
- UMDF 对象 WDK，基本对象
- 框架对象 WDK UMDF，基本对象
- 基本对象 WDK UMDF
- IWDFObject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd82c447b71c35d354f5b9daf0f72575e041a065
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815719"
---
# <a name="framework-base-object"></a>框架基对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

通过 [IWDFObject](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject) 接口向驱动程序公开框架基对象。 它提供跨所有框架对象类型通用的基本功能。 所有框架对象均派生自此根对象。

当驱动程序通过调用 [**IWDFDriver：： CreateWdfObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject) 方法创建框架基对象时，它们最初可以注册其 [IObjectCleanup](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup) 接口，以便在要销毁对象时，框架会通知驱动程序。 稍后，驱动程序可以使用 [**IWDFObject：： AssignContext**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext) 方法更改它们在框架基对象实例上接收通知的方式。

 

