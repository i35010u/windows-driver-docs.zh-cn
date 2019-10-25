---
title: NDKPI 侦听器、连接器和终结点
description: 本部分介绍了连接器和终结点的 NDKPI 侦听器、连接器、终结点和引用计数
ms.assetid: 956D3550-11C8-48D0-BCF4-9027515C7C0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd82fbeb957402088d81e7c6c2ca88b8c2ac7815
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831896"
---
# <a name="ndkpi-listeners-connectors-and-endpoints"></a>NDKPI 侦听器、连接器和终结点


NDK 使用者通过调用*NdkConnect* （[*ndk\_fn\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)）或*NdkConnectWithSharedEndpoint* （[*ndk\_FN\_使用\_共享\_连接\_来连接 ndk 连接器终结点*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)）函数。

处于连接状态的每个连接器还具有一个基础终结点，该终结点表示已建立的 NDK 连接的本地端：

-   通过在 NDK 侦听器上接受传入连接而建立的连接器会自动继承侦听器的隐式终结点作为其本地隐式终结点。
-   通过*NdkConnect*函数连接的连接器有自己专用的隐式本地终结点。
-   通过*NdkConnectWithSharedEndpoint*函数连接的连接器具有一个显式的本地终结点，该终结点可以与也通过*NdkConnectWithSharedEndpoint*函数连接的其他连接器共享。

当引用计数达到零时，NDK 提供程序必须为每个隐式或显式终结点保留某种类型的引用计数，并释放终结点（即，将地址/端口标记为可供再次使用）：

### <a name="reference-counting-for-non-shared-endpoints"></a>（非共享）终结点的引用计数

当使用者调用*NdkListen* （[*NDK\_FN\_侦听*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_listen)）函数时，提供程序会创建一个隐式终结点。 对于此隐式终结点，提供程序必须维护引用计数，如下所示：

-   将侦听器本身的引用添加到终结点的引用计数。
-   为通过该侦听器接受的每个连接器添加引用。
-   如果关闭了之前通过侦听器接受的连接器，则删除引用。
-   当侦听器本身关闭时删除引用。
    **请注意**  在关闭所有连接器之前无法关闭侦听器。

     

-   当终结点的引用计数返回为零时释放它。 （仅当侦听器和侦听器接受的所有连接器都已关闭时才是这种情况。）
-   只关闭侦听器并不会释放终结点，只要以前已有的已接受连接器尚未关闭。 这意味着，在关闭所有此类连接之前，新的*NdkListen*、 *NdkConnect*和*NdkConnectWithSharedEndpoint*请求将会失败。 请注意，侦听器上的关闭请求也将保持挂起状态，直到关闭所有此类连接（因为[NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md)中概述了前面的/后续规则）。 发出 close 请求后，该提供程序必须在侦听器上拒绝进一步的传入连接（这样，关闭请求处于挂起状态时将不接受任何新连接）。

### <a name="reference-counting-for-connectors"></a>连接器的引用计数

当使用者调用*NdkConnect*时，提供程序会创建和隐式终结点。 对于此隐式终结点，提供程序必须：

-   通过连接器添加引用。 只有一个连接器，因此只能有一个引用。
-   关闭连接器时，删除连接器对终结点的引用。
-   在该引用不存在时释放终结点。

### <a name="reference-counting-for-shared-endpoints"></a>共享终结点的引用计数

当使用者调用*NdkConnectWithSharedEndpoint*时，提供程序会创建一个显式共享终结点。 对于此显式共享终结点，提供程序必须：

-   将共享终结点自身的引用添加到共享终结点的引用计数。
-   为通过该共享终结点连接的每个连接器添加引用。
-   当以前通过共享终结点连接的连接器关闭时，删除引用。
-   释放终结点，引用计数将返回到零。 （如果共享终结点和通过共享端点连接的所有连接器都已关闭，则会出现这种情况。）
-   只要关闭共享端点，就不会释放端点，只要以前连接的连接器尚未关闭。 这意味着，在关闭所有此类连接之前，新的*NdkListen*、 *NdkConnect*和*NdkConnectWithSharedEndpoint*请求将会失败。 请注意，共享终结点上的关闭请求也将保持挂起状态，直到所有此类连接关闭（由于[NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md)中所述的前面的/后续规则）。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






