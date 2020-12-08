---
title: 使用中继器
description: 使用中继器
keywords:
- 中继器，使用中继器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 855feff1ad6323ca280d9ea6435e7cf4aacd7728
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803201"
---
# <a name="using-a-repeater"></a>使用中继器


## <span id="ddk_using_a_repeater_dbg"></span><span id="DDK_USING_A_REPEATER_DBG"></span>


中继站连接服从非常简单的规则：

-   服务器和客户端想要彼此进行的所有通信都将通过中继器，而不会改变。

-   服务器针对传输连接执行的任何操作都会影响中继器 (，只会间接影响客户端) 。

-   客户端对传输连接执行的任何操作都会影响中继器 (，只会间接影响服务器) 。

这意味着，只要客户端和服务器直接连接，就会发生任何调试命令、调试器输出、控制键和文件访问。 此中继器对于所有这些命令均不可见。

终止连接本身的操作将影响中继器。 例如，如果发出 [**qq (退出**](q--qq--quit-.md) 客户端) 命令，服务器将关闭，并将关闭信号发送到传输。 这将导致 repeater (退出，除非已通过 **-p** 选项) 启动。 作为另一个示例， [**客户端 (列出调试客户端)**](-clients--list-debugging-clients-.md) 命令将列出客户端的计算机名称，但它会显示用于将服务器与中继器连接的连接协议。

如果服务器关闭，则中继器会自动退出 (，除非它是通过 **-p** 选项) 启动的。 当中继器关闭时，这会导致调试客户端也退出，尽管智能客户端将不会退出。 如果由于某种原因而需要直接终止中继器，可以使用任务管理器或 kill.exe 工具。

 

 





