---
title: 框架驱动程序对象
description: 框架驱动程序对象
keywords:
- UMDF 对象 WDK，驱动程序对象
- framework 对象 WDK UMDF，驱动程序对象
- 驱动对象 WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1236cb01de3e4ea7f4a62fd8ec50c2afb547881
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795243"
---
# <a name="framework-driver-object"></a>框架驱动程序对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架驱动程序对象由 [IWDFDriver](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 接口向驱动程序公开。 它是驱动程序主机进程中加载的驱动程序映像的框架表示形式。 框架为驱动程序主机进程中加载的每个驱动程序创建一个新的驱动程序对象。 **IWDFDriver** 接口由 [**IDriverEntry：： OnInitialize**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法传递给驱动程序，后者是用户模式驱动程序的主入口点。

 

