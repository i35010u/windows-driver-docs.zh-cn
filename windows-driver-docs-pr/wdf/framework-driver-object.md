---
title: 框架驱动程序对象
description: 框架驱动程序对象
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF 对象 WDK，驱动程序对象
- framework 对象 WDK UMDF，驱动程序对象
- 驱动对象 WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a75e21f13f493e867161a448f12cb064b20c0d8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193127"
---
# <a name="framework-driver-object"></a>框架驱动程序对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架驱动程序对象由 [IWDFDriver](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 接口向驱动程序公开。 它是驱动程序主机进程中加载的驱动程序映像的框架表示形式。 框架为驱动程序主机进程中加载的每个驱动程序创建一个新的驱动程序对象。 **IWDFDriver**接口由[**IDriverEntry：： OnInitialize**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法传递给驱动程序，后者是用户模式驱动程序的主入口点。

 

