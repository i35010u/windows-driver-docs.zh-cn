---
title: R （Windows 调试器术语表）
description: 词汇表 page-R
ms.assetid: 77bd1a66-39b3-4990-801e-4192a6e9cf47
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee55b85f9cb6a48a95cd8c0ac63d599c4de9c1f2
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387074"
---
# <a name="r"></a>R


<span id="remote_debugging"></span><span id="REMOTE_DEBUGGING"></span>**远程调试**  
远程调试是使用远程连接执行调试的做法。

由于用户模式调试通常是在一台计算机上进行的，因此远程用户模式调试通常使用两台计算机。 在此方案中，一台计算机包含目标应用程序和调试服务器，而另一台计算机包含调试客户端。 另一种方法是在一台计算机上创建目标应用程序和进程服务器，并在另一台计算机上安装智能客户端。

由于内核模式调试通常是在两台计算机上进行的，因此远程内核模式调试需要三台计算机。 目标计算机是正在调试的计算机。 服务器已附加到目标;它包含内核模式调试器。 客户端是远程控制会话的计算机。 通常，一台计算机正在被调试，另一个计算机包含调试服务器，第三台计算机包含调试客户端。

此外，还有其他一些远程调试方法：使用远程工具、使用 KD 连接服务器或使用中继器。 你应选择哪种方法取决于相关计算机的配置以及可用连接。

有关详细信息，请参阅[远程调试](remote-debugging.md)。

<span id="register"></span><span id="REGISTER"></span>**注册**  
CPU 中速度非常快的临时内存位置。

<span id="register_context"></span><span id="REGISTER_CONTEXT"></span>**注册上下文**  
包含处理器所有寄存器的完整处理器状态。

有关详细信息，请参阅[**注册上下文**](-thread--set-register-context-.md)。

<span id="retail_build"></span><span id="RETAIL_BUILD"></span>**零售版本**  
请参阅免费构建。

 

 





