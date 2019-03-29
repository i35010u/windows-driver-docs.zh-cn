---
title: 在 UMDF 中获取有关常规 I/O 目标的信息
description: 在 UMDF 中获取有关常规 I/O 目标的信息
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 常规 I/O 有关面向 WDK UMDF，信息
- 状态信息 WDK I/O 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd1432c0b732ff18af2a950f8bea2af0da8f7625
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564192"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>在 UMDF 中获取有关常规 I/O 目标的信息


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

若要获取的 I/O 目标有关的信息，请 UMDF 驱动程序可以调用 I/O 目标对象定义的以下方法：

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget::GetTargetFile**](https://msdn.microsoft.com/library/windows/hardware/ff559243)  
返回与 I/O 目标相关联的框架文件对象。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff559202)  
返回的状态信息的本地 I/O 目标。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff560265)  
返回的状态信息的远程 I/O 目标。

 

 





