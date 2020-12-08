---
title: 硬件资源的框架对象
description: 硬件资源的框架对象
keywords:
- 硬件资源 WDK KMDF，框架对象
- framework 对象 WDK KMDF，硬件资源
- 框架资源需求-列表对象 WDK KMDF
- 框架资源范围-列表对象 WDK KMDF
- 框架资源列表对象 WDK KMDF
- 资源列表对象 WDK KMDF
- 资源范围列表对象 WDK KMDF
- 资源需求-列表对象 WDK KMDF
- 硬件资源 WDK KMDF，指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9976ad235193fe1d3776a86a0a131e8ef57fb9c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814769"
---
# <a name="framework-objects-for-hardware-resources"></a>硬件资源的框架对象


框架定义以下三个对象，框架和驱动程序使用该对象来指定设备的硬件资源：

<a href="" id="framework-resource-requirements-list-objects"></a>*框架资源需求-列表对象*  
每个框架资源需求列表对象都表示一个 [资源需求列表](../kernel/hardware-resources.md)。 这些对象的句柄的类型为 WDFIORESREQLIST。 对象定义 [框架资源需求列表对象方法](/windows-hardware/drivers/ddi/wdfresource/)。 资源要求列表由一组逻辑配置组成。

<a href="" id="framework-resource-range-list-objects"></a>*框架资源范围列表对象*  
每个框架资源范围列表对象都表示一个 [逻辑配置](../kernel/hardware-resources.md#ddk-logical-configurations-kg) (即，一组资源，设备能够使用资源需求列表中) 。 这些对象的句柄的类型为 WDFIORESLIST。 对象定义 [框架资源范围列表对象方法](/windows-hardware/drivers/ddi/wdfresource/)。

<a href="" id="framework-resource-list-objects"></a>*框架资源列表对象*  
每个框架资源列表对象都表示一个逻辑配置 (即 [资源列表](../kernel/hardware-resources.md)中) 一组特定资源。 这些对象的句柄的类型为 WDFCMRESLIST。 对象定义 [框架资源列表对象方法](/windows-hardware/drivers/ddi/wdfresource/)。

 

