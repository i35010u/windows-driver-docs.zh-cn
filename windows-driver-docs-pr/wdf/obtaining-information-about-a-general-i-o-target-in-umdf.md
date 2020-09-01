---
title: 在 UMDF 中获取有关常规 I/O 目标的信息
description: 在 UMDF 中获取有关常规 I/O 目标的信息
ms.assetid: 306a7f46-423a-4647-846d-76f917ca0f7c
keywords:
- 一般 i/o 目标为 WDK UMDF，有关
- 状态信息 WDK i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e66206f1d6a4f021d3f389adbcf29f34627d28a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184621"
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

 

