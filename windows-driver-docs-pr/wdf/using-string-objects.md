---
title: 使用字符串对象
description: 本主题介绍 Windows 驱动程序框架（WDF）为字符串对象提供的支持。 它同时适用于内核模式驱动程序框架（KMDF）。
ms.assetid: b1d52a18-ebd5-4ba7-b5c7-3ef3d298c82e
keywords:
- 字符串对象 WDK KMDF
- framework 对象 WDK KMDF，string 对象
- Unicode 字符串 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7be4d5f23261f44ca2abb04272355093f1e832a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845426"
---
# <a name="using-string-objects"></a>使用字符串对象


本主题介绍 Windows 驱动程序框架（WDF）为字符串对象提供的支持。 它适用于从版本2开始的内核模式驱动程序框架（KMDF）驱动程序和用户模式驱动程序框架（UMDF）驱动程序。




WDF 仅使用 Unicode 字符串。 框架对象定义的所有方法仅接受 Unicode 字符串。

框架定义了 KMDF 和 UMDF 驱动程序可用于表示 Unicode 字符串的*框架字符串对象*。

驱动程序可以调用[**WdfStringCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringcreate)来创建字符串对象并根据需要将 Unicode 字符串分配给对象。

某些框架对象方法（如[**WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerystring)）接受字符串对象句柄作为输入，并将字符串分配给 string 对象。

若要访问分配给 string 对象的字符串，驱动程序可以调用[**WdfStringGetUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfstring/nf-wdfstring-wdfstringgetunicodestring)。

 

 





