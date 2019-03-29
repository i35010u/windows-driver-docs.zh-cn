---
title: NDKPI 侦听器、 连接器和终结点
description: 本部分介绍 NDKPI 侦听器、 连接器和终结点和引用计数为连接器和终结点
ms.assetid: 956D3550-11C8-48D0-BCF4-9027515C7C0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 192f287d210db880df875b6a8e8a6daeb737bf19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564794"
---
# <a name="ndkpi-listeners-connectors-and-endpoints"></a>NDKPI 侦听器、连接器和终结点


NDK 使用者通过调用连接 NDK 连接器*NdkConnect* ([*NDK\_FN\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/hh439865)) 或*NdkConnectWithSharedEndpoint* ([*NDK\_FN\_CONNECT\_WITH\_共享\_终结点*](https://msdn.microsoft.com/library/windows/hardware/hh439868)) 函数。

处于连接状态的每个连接器还具有基础终结点，表示已建立的 NDK 连接的本地端：

-   建立通过自动 NDK 侦听器通过接受传入连接的连接器作为其本地的隐式终结点将继承该侦听器的隐式终结点。
-   通过连接的连接器*NdkConnect*函数具有其自己专用的隐式本地终结点。
-   通过连接的连接器*NdkConnectWithSharedEndpoint*函数具有显式本地终结点可以与其他连接器还通过连接共享*NdkConnectWithSharedEndpoint*函数。

NDK 提供程序必须保持某种形式的每个隐式或显式终结点，引用计数和发布终结点 （即，将标记为可用，再次使用地址/端口） 的引用计数达到零时时：

### <a name="reference-counting-for-non-shared-endpoints"></a>引用计数 （非共享） 终结点

当使用者调用*NdkListen* ([*NDK\_FN\_侦听*](https://msdn.microsoft.com/library/windows/hardware/hh439902)) 函数，该提供程序创建的隐式终结点。 对于此隐式的终结点，该提供程序必须维护的引用计数，如下所示：

-   添加侦听器本身终结点的引用计数的引用。
-   添加为该侦听器通过接受每个连接器的引用。
-   关闭以前已通过侦听器接受的连接器时，请删除引用。
-   关闭侦听器本身时，请删除引用。
    **请注意**  之前关闭所有连接器无法关闭侦听器。

     

-   发布终结点时其引用计数归零。 （这是这种情况仅通过侦听器时接受侦听器和所有连接器已关闭。）
-   只需关闭该侦听器不会释放该终结点，只要以前已接受但尚未关闭的连接器。 这意味着新*NdkListen*， *NdkConnect*，并*NdkConnectWithSharedEndpoint*请求相同的本地地址和端口将失败，直至所有此类连接已关闭。 请注意对侦听程序的关闭请求也将保持挂起状态直到所有此类连接已关闭 (由于前面的任务/后续规则中所述[NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md))。 提供程序必须拒绝对侦听程序传入的其他连接，就立即关闭请求发出 （以便关闭请求挂起时，将接受任何新连接）。

### <a name="reference-counting-for-connectors"></a>引用计数的连接器

当使用者调用*NdkConnect*，提供程序创建和隐式终结点。 对于此隐式的终结点，该提供程序必须：

-   添加连接器的引用。 没有只有一个连接器，因此只有一个引用。
-   关闭连接器时，请删除对该终结点的连接器的引用。
-   发布终结点时，引用将消失。

### <a name="reference-counting-for-shared-endpoints"></a>引用计数为共享的终结点

当使用者调用*NdkConnectWithSharedEndpoint*，提供程序创建显式共享终结点。 对于此显式共享的终结点，该提供程序必须：

-   将共享终结点自身的引用添加到共享终结点的引用计数。
-   添加该共享的终结点通过连接每个连接器的引用。
-   关闭之前已通过共享终结点连接的连接器时，请删除引用。
-   发布终结点引用计数归零。 （这是这种情况时已关闭共享终结点并通过共享终结点连接的所有连接器。）
-   只需关闭共享终结点不会释放该终结点，只要有之前连接尚未解决的连接器。 这意味着新*NdkListen*， *NdkConnect*，并*NdkConnectWithSharedEndpoint*请求相同的本地地址和端口将失败，直至所有此类连接已关闭。 请注意共享终结点上的关闭请求也将保持挂起状态直到所有此类连接已关闭 (由于前面的任务/后续规则中所述[NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md))。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






