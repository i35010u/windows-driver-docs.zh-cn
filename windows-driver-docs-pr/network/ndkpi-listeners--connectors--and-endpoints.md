---
title: NDKPI 侦听器、连接器和终结点
description: 本部分介绍了连接器和终结点的 NDKPI 侦听器、连接器、终结点和引用计数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 475aa8bae6018acc9e2f2c93d8364451658cfd27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839879"
---
# <a name="ndkpi-listeners-connectors-and-endpoints"></a>NDKPI 侦听器、连接器和终结点


NDK 使用者通过调用 *NdkConnect* ([*ndk \_ Fn \_ Connect*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)) 或 *NdkConnectWithSharedEndpoint* ([*ndk \_ fn \_ connect \_ WITH \_ SHARED \_ ENDPOINT*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_with_shared_endpoint)) 函数连接到 ndk 连接器。

处于连接状态的每个连接器还具有一个基础终结点，该终结点表示已建立的 NDK 连接的本地端：

-   通过在 NDK 侦听器上接受传入连接而建立的连接器会自动继承侦听器的隐式终结点作为其本地隐式终结点。
-   通过 *NdkConnect* 函数连接的连接器有自己专用的隐式本地终结点。
-   通过 *NdkConnectWithSharedEndpoint* 函数连接的连接器具有一个显式的本地终结点，该终结点可以与也通过 *NdkConnectWithSharedEndpoint* 函数连接的其他连接器共享。

对于每个隐式或显式终结点，NDK 提供程序必须保留某种引用计数，并释放终结点， (例如，将该地址/端口标记为可在引用计数达到零时再次使用) ：

### <a name="reference-counting-for-non-shared-endpoints"></a> (非共享) 端点的引用计数

当使用者调用 *NdkListen* 时 ([*NDK \_ FN \_ 侦听*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_listen)) 函数时，提供程序会创建一个隐式终结点。 对于此隐式终结点，提供程序必须维护引用计数，如下所示：

-   将侦听器本身的引用添加到终结点的引用计数。
-   为通过该侦听器接受的每个连接器添加引用。
-   如果关闭了之前通过侦听器接受的连接器，则删除引用。
-   当侦听器本身关闭时删除引用。
    **注意**  在关闭所有连接器之前，无法关闭侦听器。

     

-   当终结点的引用计数返回为零时释放它。 仅当侦听器和侦听器上接受的所有连接器都已关闭时，才 (这种情况。 ) 
-   只关闭侦听器并不会释放终结点，只要以前已有的已接受连接器尚未关闭。 这意味着，在关闭所有此类连接之前，新的 *NdkListen*、 *NdkConnect* 和 *NdkConnectWithSharedEndpoint* 请求将会失败。 请注意，侦听器上的关闭请求也将保持挂起状态，直到所有此类连接 (关闭，因为 [NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md)) 中列出了前面的前面/后续规则。 发出 close 请求后，该提供程序必须在侦听器上拒绝进一步的传入连接 (这样，当关闭请求处于挂起状态时，就不会接受新的连接) 。

### <a name="reference-counting-for-connectors"></a>连接器的引用计数

当使用者调用 *NdkConnect* 时，提供程序会创建和隐式终结点。 对于此隐式终结点，提供程序必须：

-   通过连接器添加引用。 只有一个连接器，因此只能有一个引用。
-   关闭连接器时，删除连接器对终结点的引用。
-   在该引用不存在时释放终结点。

### <a name="reference-counting-for-shared-endpoints"></a>共享终结点的引用计数

当使用者调用 *NdkConnectWithSharedEndpoint* 时，提供程序会创建一个显式共享终结点。 对于此显式共享终结点，提供程序必须：

-   将共享终结点自身的引用添加到共享终结点的引用计数。
-   为通过该共享终结点连接的每个连接器添加引用。
-   当以前通过共享终结点连接的连接器关闭时，删除引用。
-   释放终结点，引用计数将返回到零。  (如果共享终结点和通过共享终结点连接的所有连接器都已关闭，则会出现此情况。 ) 
-   只要关闭共享端点，就不会释放端点，只要以前连接的连接器尚未关闭。 这意味着，在关闭所有此类连接之前，新的 *NdkListen*、 *NdkConnect* 和 *NdkConnectWithSharedEndpoint* 请求将会失败。 请注意，共享终结点上的关闭请求也将保持挂起状态，直到关闭所有此类连接 (因为 [NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md)) 中列出的前面的任务或后续规则。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

