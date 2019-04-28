---
title: 激活安全模式
description: 激活安全模式
ms.assetid: bb7cd081-f032-4af4-bb4d-efa96917088b
keywords:
- 安全模式下，如何激活
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc2807ce8c10d103b59eb6818cb985024fbb0976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354415"
---
# <a name="activating-secure-mode"></a>激活安全模式


## <span id="ddk_activating_secure_mode_dbg"></span><span id="DDK_ACTIVATING_SECURE_MODE_DBG"></span>


安全模式功能仅适用于内核模式调试。 必须先在调试会话已开始-在调试器的命令行上或调试器是完全处于休眠状态且不尚未使用时为服务器激活它。

若要激活安全模式下，使用以下方法之一：

-   **的安全**[命令行选项](command-line-options.md)

-   [ **.Secure 1** ](-secure--activate-secure-mode-.md)命令

-   [ **.Symopt + 而 0x40000 可**](-symopt--set-symbol-options-.md)命令

如果有现有的内核调试会话并需要发现您是否已在安全模式下，使用[ **.secure** ](-secure--activate-secure-mode-.md)命令不带任何参数。 它将告诉您的安全模式下的当前状态。

激活安全模式后，它不能已关闭。 甚至终止调试会话将不将其关闭。 安全模式下仍然存在，只要运行调试器本身。

 

 





