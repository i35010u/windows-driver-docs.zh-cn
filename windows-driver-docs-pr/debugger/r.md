---
title: R （Windows 调试器词汇表）
description: 术语表页-R
Robots: noindex, nofollow
ms.assetid: 77bd1a66-39b3-4990-801e-4192a6e9cf47
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86867e78f0da56f9458801e53829532a5f3c6ea1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335538"
---
# <a name="r"></a>R


<span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>**远程调试**  
远程调试是一种使用远程连接来执行调试行为。

由于用户模式下调试通常是一台计算机上，远程用户模式下调试通常使用两台计算机。 在此方案中，一台计算机包含目标应用程序和调试服务器，而另一台计算机包含调试客户端。 另一种方法是具有目标应用程序和一台计算机上的进程服务器和另一个智能客户端。

因为内核模式调试通常是在两台计算机上，远程内核模式调试需要三台计算机。 目标计算机是正在调试的计算机。 将服务器附加到目标;它包含内核模式调试程序。 客户端的计算机的远程控制会话。 通常情况下，一台计算机是正在调试，另一个包含调试服务器和第三个包含调试客户端。

此外，还有其他方法的远程调试： 使用远程工具、 使用 KD 连接服务器，或使用 repeater。 应选择的方法取决于有问题的计算机和可用连接的配置。

有关详细信息，请参阅[远程调试](remote-debugging.md)。

<span id="register"></span><span id="REGISTER"></span>**register**  
中 CPU 的非常快的临时内存位置。

<span id="register_context"></span><span id="REGISTER_CONTEXT"></span>**注册上下文**  
使用完整处理器状态，其中包括所有处理器的寄存器。

有关详细信息，请参阅[**注册上下文**](-thread--set-register-context-.md)。

<span id="retail_build"></span><span id="RETAIL_BUILD"></span>**零售版本**  
请参阅免费生成。

 

 





