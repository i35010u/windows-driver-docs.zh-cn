---
title: Framework 驱动程序对象
description: Framework 驱动程序对象
ms.assetid: 6e9e568c-7e4f-48bd-b351-4be0e12cc15b
keywords:
- UMDF 对象 WDK，驱动程序对象
- framework 对象 WDK UMDF，驱动程序对象
- 驱动程序对象 WDK UMDF
- IWDFDriver
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 263c5b5005fbc9d99c28ffca6b179306a60c35ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543105"
---
# <a name="framework-driver-object"></a>Framework 驱动程序对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework 驱动程序对象[IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)接口。 它是驱动程序主机进程中加载的驱动程序映像的 framework 表示形式。 框架将创建一个新的驱动程序在驱动程序主机进程中加载每个驱动程序对象。 **IWDFDriver**接口传递给驱动程序[ **IDriverEntry::OnInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff554900)方法，它是用户模式驱动程序的主入口点。

 

 





