---
title: 激活安全模式
description: 激活安全模式
keywords:
- 安全模式，激活方式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19dc03912aa81bbaec4e8fb31d6a1aba54e7dd62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796302"
---
# <a name="activating-secure-mode"></a>激活安全模式


## <span id="ddk_activating_secure_mode_dbg"></span><span id="DDK_ACTIVATING_SECURE_MODE_DBG"></span>


安全模式仅适用于内核模式调试。 它必须在调试会话开始之前激活--在调试器的命令行上，或者当调试器完全处于休眠状态并且尚未用作服务器时，必须激活。

若要激活安全模式，请使用下列方法之一：

-   **-Secure** [命令行选项](command-line-options.md)

-   [**Secure 1**](-secure--activate-secure-mode-.md)命令

-   [**Symopt + 0x40000**](-symopt--set-symbol-options-.md)命令

如果你有现有的内核调试会话，并且需要发现你是否已处于安全模式，请使用不带参数的 [**secure**](-secure--activate-secure-mode-.md) 命令。 这将告知当前安全模式的状态。

激活安全模式后，将无法关闭。 即使结束调试会话也不会将其关闭。 只要调试器本身正在运行，安全模式就会保持不变。

 

 





