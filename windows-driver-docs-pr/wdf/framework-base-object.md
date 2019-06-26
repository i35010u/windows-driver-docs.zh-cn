---
title: 框架基对象
description: 框架基对象
ms.assetid: 9d400192-faf0-4d8f-849b-6b955105e21a
keywords:
- UMDF 对象 WDK，基对象
- framework 对象 WDK UMDF，基对象
- 基对象 WDK UMDF
- IWDFObject
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6587b58b85a5d32710cb4ff16b620c63460c1541
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368685"
---
# <a name="framework-base-object"></a>框架基对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework 基对象[IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)接口。 它提供跨所有 framework 对象类型是公共的基本功能。 Framework 的所有对象均都源自此根对象。

驱动程序时创建框架基对象通过调用[ **IWDFDriver::CreateWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)方法，用户可以最初在注册其[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iobjectcleanup)接口，以便在 framework 即将销毁对象时通知该驱动程序。 驱动程序可以使用更高版本， [ **IWDFObject::AssignContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-assigncontext)方法来更改他们如何接收 framework 基对象实例上的通知。

 

 





