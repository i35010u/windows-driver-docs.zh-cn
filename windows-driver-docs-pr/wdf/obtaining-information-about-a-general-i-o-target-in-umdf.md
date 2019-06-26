---
title: 在 UMDF 中获取有关常规 I/O 目标的信息
description: 在 UMDF 中获取有关常规 I/O 目标的信息
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 常规 I/O 有关面向 WDK UMDF，信息
- 状态信息 WDK I/O 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b28de8a49820c4fad51b2dfb29859d506ccb24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375090"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>在 UMDF 中获取有关常规 I/O 目标的信息


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

若要获取的 I/O 目标有关的信息，请 UMDF 驱动程序可以调用 I/O 目标对象定义的以下方法：

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget::GetTargetFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile)  
返回与 I/O 目标相关联的框架文件对象。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)  
返回的状态信息的本地 I/O 目标。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)  
返回的状态信息的远程 I/O 目标。

 

 





