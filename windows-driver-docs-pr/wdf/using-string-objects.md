---
title: 使用字符串对象
description: 本主题介绍 Windows 驱动程序框架 (WDF) 为字符串对象提供的支持。 它同时适用于 Kernel-Mode Driver Framework (KMDF) 。
keywords:
- 字符串对象 WDK KMDF
- framework 对象 WDK KMDF，string 对象
- Unicode 字符串 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e4802a7b51663811487f856d98ed98228651050
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827393"
---
# <a name="using-string-objects"></a>使用字符串对象


本主题介绍 Windows 驱动程序框架 (WDF) 为字符串对象提供的支持。 它适用于从版本2开始 Kernel-Mode Driver Framework (KMDF) 驱动程序和 User-Mode Driver Framework (UMDF) 驱动程序。




WDF 仅使用 Unicode 字符串。 框架对象定义的所有方法仅接受 Unicode 字符串。

框架定义了 KMDF 和 UMDF 驱动程序可用于表示 Unicode 字符串的 *框架字符串对象* 。

驱动程序可以调用 [**WdfStringCreate**](/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate) 来创建字符串对象并根据需要将 Unicode 字符串分配给对象。

某些框架对象方法（如 [**WdfRegistryQueryString**](/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerystring)）接受字符串对象句柄作为输入，并将字符串分配给 string 对象。

若要访问分配给 string 对象的字符串，驱动程序可以调用 [**WdfStringGetUnicodeString**](/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringgetunicodestring)。

 

