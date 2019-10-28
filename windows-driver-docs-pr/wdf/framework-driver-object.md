---
title: Framework 驱动程序对象
description: Framework 驱动程序对象
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF 对象 WDK，驱动程序对象
- framework 对象 WDK UMDF，驱动程序对象
- 驱动对象 WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9dd791dd23c12aed943278006bcc1b4a743165e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843179"
---
# <a name="framework-driver-object"></a>Framework 驱动程序对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架驱动程序对象由[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)接口向驱动程序公开。 它是驱动程序主机进程中加载的驱动程序映像的框架表示形式。 框架为驱动程序主机进程中加载的每个驱动程序创建一个新的驱动程序对象。 **IWDFDriver**接口由[**IDriverEntry：： OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)方法传递给驱动程序，后者是用户模式驱动程序的主入口点。

 

 





