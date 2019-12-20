---
title: 框架基对象
description: 框架基对象
ms.assetid: 9d400192-faf0-4d8f-849b-6b955105e21a
keywords:
- UMDF 对象 WDK，基本对象
- 框架对象 WDK UMDF，基本对象
- 基本对象 WDK UMDF
- IWDFObject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca01979829858282d761f17e4e94a8e901ef2e4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210755"
---
# <a name="framework-base-object"></a>框架基对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

通过[IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)接口向驱动程序公开框架基对象。 它提供跨所有框架对象类型通用的基本功能。 所有框架对象均派生自此根对象。

当驱动程序通过调用[**IWDFDriver：： CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)方法创建框架基对象时，它们最初可以注册其[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup)接口，以便在要销毁对象时，框架会通知驱动程序。 稍后，驱动程序可以使用[**IWDFObject：： AssignContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)方法更改它们在框架基对象实例上接收通知的方式。

 

 





