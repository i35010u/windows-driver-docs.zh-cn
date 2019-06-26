---
title: 使用字符串对象
description: 本主题介绍 Windows 驱动程序框架 (WDF) 的字符串对象提供的支持。 它将应用到这两个内核模式驱动程序框架 (KMDF)。
ms.assetid: b1d52a18-ebd5-4ba7-b5c7-3ef3d298c82e
keywords:
- 字符串对象 WDK KMDF
- framework 对象 WDK KMDF，字符串对象
- Unicode 字符串 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c84f1261ac9b812ef5e4aee8d33c15aa15a83f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372211"
---
# <a name="using-string-objects"></a>使用字符串对象


本主题介绍 Windows 驱动程序框架 (WDF) 的字符串对象提供的支持。 它适用于内核模式驱动程序框架 (KMDF) 驱动程序和用户模式驱动程序框架 (UMDF) 驱动程序从版本 2。




WDF 仅使用 Unicode 字符串。 所有由 framework 对象定义的方法只接受 Unicode 字符串。

该框架定义*framework 字符串对象*KMDF 和 UMDF 驱动程序可以使用来表示 Unicode 字符串。

您的驱动程序可以调用[ **WdfStringCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/nf-wdfstring-wdfstringcreate)创建字符串对象，可以选择为该对象指定的 Unicode 字符串。

某些框架的对象的方法，例如[ **WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerystring)，接受作为输入的字符串对象句柄并将字符串分配字符串对象。

若要访问分配给一个字符串对象的字符串，您的驱动程序可以调用[ **WdfStringGetUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfstring/nf-wdfstring-wdfstringgetunicodestring)。

 

 





