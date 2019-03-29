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
ms.openlocfilehash: f1ac10b79e7937af15051f4702bba69ac0639dd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565246"
---
# <a name="framework-base-object"></a>框架基对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework 基对象[IWDFObject](https://msdn.microsoft.com/library/windows/hardware/ff560200)接口。 它提供跨所有 framework 对象类型是公共的基本功能。 Framework 的所有对象均都源自此根对象。

驱动程序时创建框架基对象通过调用[ **IWDFDriver::CreateWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff558906)方法，用户可以最初在注册其[IObjectCleanup](https://msdn.microsoft.com/library/windows/hardware/ff556754)接口，以便在 framework 即将销毁对象时通知该驱动程序。 驱动程序可以使用更高版本， [ **IWDFObject::AssignContext** ](https://msdn.microsoft.com/library/windows/hardware/ff560208)方法来更改他们如何接收 framework 基对象实例上的通知。

 

 





