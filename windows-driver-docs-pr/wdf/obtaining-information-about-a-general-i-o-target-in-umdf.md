---
title: 在 UMDF 中获取有关常规 I/O 目标的信息
description: 在 UMDF 中获取有关常规 I/O 目标的信息
keywords:
- 一般 i/o 目标为 WDK UMDF，有关
- 状态信息 WDK i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13027f5da7db51ea4948232f0461ab2a1bc5e7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839339"
---
# <a name="obtaining-information-about-a-general-io-target-in-umdf"></a>在 UMDF 中获取有关常规 I/O 目标的信息


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

若要获取有关 i/o 目标的信息，UMDF 驱动程序可以调用 i/o 目标对象定义的以下方法：

<a href="" id="iwdfiotarget--gettargetfile"></a>[**IWDFIoTarget::GetTargetFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-gettargetfile)  
返回与 i/o 目标相关联的框架文件对象。

<a href="" id="iwdfiotargetstatemanagement--getstate"></a>[**IWDFIoTargetStateManagement：： GetState**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)  
返回本地 i/o 目标的状态信息。

<a href="" id="iwdfremotetarget--getstate"></a>[**IWDFRemoteTarget：： GetState**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-getstate)  
返回远程 i/o 目标的状态信息。

 

