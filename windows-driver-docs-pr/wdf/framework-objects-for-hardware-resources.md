---
title: 硬件资源的框架对象
description: 硬件资源的框架对象
ms.assetid: 64eb628f-ce3d-494b-9fc1-7179a722c5f2
keywords:
- 硬件资源 WDK KMDF，framework 对象
- framework 对象 WDK KMDF，硬件资源
- framework 资源要求列表对象 WDK KMDF
- framework 资源范围列表对象 WDK KMDF
- 对象 WDK KMDF framework 资源的列表
- 资源列出对象 WDK KMDF
- 资源范围列表对象 WDK KMDF
- 资源要求列表对象 WDK KMDF
- WDK KMDF，指定的硬件资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a4303c4a0d0e7ef84c9c005952fa12376523fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384450"
---
# <a name="framework-objects-for-hardware-resources"></a>硬件资源的框架对象


该框架定义的框架和驱动程序使用来指定设备的硬件资源的以下三个对象：

<a href="" id="framework-resource-requirements-list-objects"></a>*Framework 资源要求列表对象*  
每个框架资源要求列表对象表示[资源要求列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)。 这些对象的句柄具有 WDFIORESREQLIST 的类型。 该对象定义[framework 资源的要求列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)。 资源要求列表包含一组逻辑配置。

<a href="" id="framework-resource-range-list-objects"></a>*Framework 资源范围列表对象*  
每个框架资源范围列表对象表示[逻辑配置](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)（即，一组的资源是否能够使用设备的范围） 中资源的要求列表。 这些对象的句柄具有 WDFIORESLIST 的类型。 该对象定义[framework 资源范围列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)。

<a href="" id="framework-resource-list-objects"></a>*Framework 资源的列表对象*  
每个框架资源列表对象中表示逻辑配置 （即，一组特定的资源）[资源列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)。 这些对象的句柄具有 WDFCMRESLIST 的类型。 该对象定义[framework 资源的列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)。

 

 





