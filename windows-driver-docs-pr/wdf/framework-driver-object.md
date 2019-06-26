---
title: 框架驱动程序对象
description: 框架驱动程序对象
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF 对象 WDK，驱动程序对象
- framework 对象 WDK UMDF，驱动程序对象
- 驱动程序对象 WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c9a5f69d1cefcf9c61f657fd3d6af14f9ab3c7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368666"
---
# <a name="framework-driver-object"></a>框架驱动程序对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework 驱动程序对象[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)接口。 它是驱动程序主机进程中加载的驱动程序映像的 framework 表示形式。 框架将创建一个新的驱动程序在驱动程序主机进程中加载每个驱动程序对象。 **IWDFDriver**接口传递给驱动程序[ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法，它是用户模式驱动程序的主入口点。

 

 





