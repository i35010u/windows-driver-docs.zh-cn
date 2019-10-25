---
title: 硬件资源的框架对象
description: 硬件资源的框架对象
ms.assetid: 64eb628f-ce3d-494b-9fc1-7179a722c5f2
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
ms.openlocfilehash: 7c10fa62675b0d58b143492f87be130af23a0ff0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845136"
---
# <a name="framework-objects-for-hardware-resources"></a>硬件资源的框架对象


框架定义以下三个对象，框架和驱动程序使用该对象来指定设备的硬件资源：

<a href="" id="framework-resource-requirements-list-objects"></a>*框架资源需求-列表对象*  
每个框架资源需求列表对象都表示一个[资源需求列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)。 这些对象的句柄的类型为 WDFIORESREQLIST。 对象定义[框架资源需求列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)。 资源要求列表由一组逻辑配置组成。

<a href="" id="framework-resource-range-list-objects"></a>*框架资源范围列表对象*  
每个框架资源范围列表对象都表示资源要求列表中的[逻辑配置](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)（即设备能够使用的一组资源范围）。 这些对象的句柄的类型为 WDFIORESLIST。 对象定义[框架资源范围列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)。

<a href="" id="framework-resource-list-objects"></a>*框架资源列表对象*  
每个框架资源列表对象都代表[资源列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)中的逻辑配置（即一组特定资源）。 这些对象的句柄的类型为 WDFCMRESLIST。 对象定义[框架资源列表对象方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)。

 

 





