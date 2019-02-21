---
title: 使用绑定或连接重定向
description: 使用绑定或连接重定向
ms.assetid: 6b27a9ad-53e9-4e80-bf03-79665f8a82a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97183ea47da2174722cac9b6316375dbb92261af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541031"
---
# <a name="using-bind-or-connect-redirection"></a>使用绑定或连接重定向


连接/绑定重定向功能的 Windows 筛选平台 (WFP) 使应用程序层强制 (ALE) 标注驱动程序，以检查和必要时，将连接重定向。

此功能是可用在 Windows 7 及更高版本。

**请注意**  ClassifyFunctions\_ProxyCallouts.cpp 模块[WFP 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618934)包括演示连接/绑定重定向的代码。

 

WFP 连接重定向标注，以便应用程序连接到代理服务，而不是原始的目标应用程序的连接请求重定向。 代理服务有两个套接字： 一个用于重定向的原始连接，一个新的代理出站连接。

WFP 重定向记录是 WFP 必须设置在出站代理服务器连接的不透明数据的缓冲区**FWPM\_层\_ALE\_身份验证\_CONNECT\_重定向\_V4**并**FWPM\_层\_ALE\_身份验证\_CONNECT\_重定向\_V6**层，以便重定向的连接逻辑上相关的原始连接。

绑定重定向是可能的因为它不需要支持中的连接重定向本地地址和端口的修改。 作为的一部分更改的本地地址和端口连接重定向不受支持。

### <a name="layers-used-for-redirection"></a>用于重定向的层

在以下图层，称为"重定向层"标注驱动程序可以执行重定向：

-   FWPM\_LAYER\_ALE\_BIND\_REDIRECT\_V4 (FWPS\_LAYER\_ALE\_BIND\_REDIRECT\_V4)

-   FWPM\_LAYER\_ALE\_BIND\_REDIRECT\_V6 (FWPS\_LAYER\_ALE\_BIND\_REDIRECT\_V6)

-   FWPM\_LAYER\_ALE\_CONNECT\_REDIRECT\_V4 (FWPS\_LAYER\_ALE\_CONNECT\_REDIRECT\_V4)

-   FWPM\_LAYER\_ALE\_CONNECT\_REDIRECT\_V6 (FWPS\_LAYER\_ALE\_CONNECT\_REDIRECT\_V6)

执行重定向的间隔的层确定更改的效果。 在 connect 层上的更改会影响连接流。 在更改绑定层会影响使用该套接字的所有连接。

重定向层才适用于 Windows 7 和更高版本的 Windows。 支持在这些层的分类的标注驱动程序必须使用注册[ **FwpsCalloutRegister1** ](https://msdn.microsoft.com/library/windows/hardware/ff551143)或更高版本，不旧[ **FwpsCalloutRegister0**](https://msdn.microsoft.com/library/windows/hardware/ff551140)函数。

> [!IMPORTANT]
> 重定向不是可用于所有类型的网络流量。 以下列表中显示的支持重定向的数据包类型：
> - TCP
> - UDP
> - 没有标头的原始 UDPv4 包括选项
> - 原始 ICMP

### <a name="performing-redirection"></a>执行重定向

若要将连接重定向，标注驱动程序必须获取 TCP 4 元组信息的可写副本，根据需要对其进行更改并应用所做的更改。 若要获取可写层数据并将其应用通过引擎提供了一组新功能。 标注驱动程序可以选择更改为内联在其[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)函数，或以异步方式在另一个函数。

实现重定向的标注驱动程序必须使用[ *classifyFn1* ](https://msdn.microsoft.com/library/windows/hardware/ff544893)或更高版本，而不是[ *classifyFn0* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)作为其分类标注函数。 若要使用*classifyFn1*或更高版本，必须通过调用注册标注[ **FwpsCalloutRegister1** ](https://msdn.microsoft.com/library/windows/hardware/ff551143)或更高版本，不旧[ **FwpsCalloutRegister0**](https://msdn.microsoft.com/library/windows/hardware/ff551140)。

若要执行重定向内联标注驱动程序必须执行以下步骤在其实现[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887):

1.  调用[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)以获取可用于 TCP 连接重定向的句柄。 应缓存，用于所有重定向此句柄。 （此步骤中省略了适用于 Windows 7 及更早版本。）

2.  在 Windows 8 和更高版本，您必须通过使用查询连接的重定向状态[ **FwpsQueryConnectionRedirectState0** ](https://msdn.microsoft.com/library/windows/hardware/hh439677)标注驱动程序中的函数。 这必须完成以防止无限重定向。

3.  调用[ **FwpsAcquireClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff550085)以获取要用于后续函数调用的句柄。

4.  调用[ **FwpsAcquireWritableLayerDataPointer0** ](https://msdn.microsoft.com/library/windows/hardware/ff550087)若要获取的可写数据结构所在的层[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)调用。 强制转换*writableLayerData* out 参数向结构对应于该层，要么[ **FWPS\_绑定\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551221)或[**FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)。

    从 Windows 8 开始，如果您的标注驱动程序将重定向到本地服务，必须调用[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)填写**localRedirectHandle**成员[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)结构以使工作的本地代理。

5.  对层数据根据需要进行更改：

    1.  在本地重定向上下文中保存的原始目标，如下面的示例中所示：

        ```C++
        FWPS_CONNECT_REQUEST* connectRequest = redirectContext->connectRequest;
        // Replace "..." with your own redirect context size
        connectRequest->localRedirectContextSize = ...;
        // Store original destination IP/Port information in the localRedirectContext member
        connectRequest->localRedirectContext =    ExAllocatePoolWithTag(…);
        ```

    2.  修改远程地址，如下面的示例中所示：

        ```C++
        // Ensure we don't need to worry about crossing any of the TCP/IP stack's zones
        if(INETADDR_ISANY((PSOCKADDR)&(connectRequest->localAddressAndPort)))
        {
           INETADDR_SETLOOPBACK((PSOCKADDR)&(connectRequest->remoteAddressAndPort));
        }
        else
        {
           INETADDR_SET_ADDRESS((PSOCKADDR)&(connectRequest->remoteAddressAndPort),
                                 INETADDR_ADDRESS((PSOCKADDR)&(connectRequest->localAddressAndPort)));
        }
        INETADDR_SET_PORT((PSOCKADDR)&connectRequest->remoteAddressAndPort,
                          RtlUshortByteSwap(params->proxyPort));
        ```

    3.  如果您的标注驱动程序将重定向到本地服务，它应设置中的本地代理 PID **localRedirectTargetPID**的成员[ **FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)结构。
    4.  如果您的标注驱动程序将重定向到本地服务，它应设置 FwpsRedirectHandleCreate0 中返回的重定向句柄**localRedirectHandle** FWPS 成员\_CONNECT\_REQUEST0结构。

6.  调用[ **FwpsApplyModifiedLayerData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551137)要应用到数据所做的更改。

7.  在代理服务中 （这可能是在用户模式或内核模式下），如下面的示例中所示，您应该查询重定向记录和上下文：

    ```C++
    BYTE* redirectRecords;
    BYTE redirectContext[CONTEXT_SIZE];
    listenSock = WSASocket(…);
    result = bind(listenSock, …);
    result = listen(listenSock, …);
    clientSock = WSAAccept(listenSock, …);
    // opaque data to be set on proxy connection
    result = WSAIoctl(clientSock,
                      SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS,
                      redirectRecords, …);
    // callout allocated data, contains original destination information
    result = WSAIoctl(clientSock,
                      SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT,
                      redirectContext, …);
    // extract original destination IP and port from above context
    ```

8.  在代理服务中 （这可能是在用户模式或内核模式下），您应在代理服务器连接套接字上设置重定向记录，若要创建新的出站套接字在下面的示例所示：

    ```C++
    proxySock = WSASocket(…);
    result = WSAIoctl(
                 proxySock,
                 SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS,
                 redirectRecords, …);
    ```

9.  调用[ **FwpsReleaseClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff551208)释放在步骤 2 中获得的分类句柄。

10. 调用[ **FwpsRedirectHandleDestroy0** ](https://msdn.microsoft.com/library/windows/hardware/hh439684)销毁已在步骤 1 中获取的句柄。

若要以异步方式执行重定向标注驱动程序必须执行以下步骤：

1.  调用[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)以获取可用于 TCP 连接重定向的句柄。 （此步骤中省略了适用于 Windows 7 及更早版本。）

2.  在 Windows 8 和更高版本，您必须通过使用查询连接的重定向状态[ **FwpsQueryConnectionRedirectState0** ](https://msdn.microsoft.com/library/windows/hardware/hh439677)标注驱动程序中的函数。

3.  调用[ **FwpsAcquireClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff550085)以获取要用于后续函数调用的句柄。 标注驱动程序中执行此步骤，步骤 2 和 3 [classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)标注函数。

4.  调用[ **FwpsPendClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551197)将分类放在挂起状态，如下面的示例中所示：

    ```C++
    FwpsPendClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_BLOCK;
    classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    ```

> [!NOTE]
> 如果你面向的 Windows 7，您必须在单独的工作函数中执行以下步骤。 如果你面向的 Windows 8 或更高版本，你可以执行所有步骤中的异步重定向*classifyFn*并忽略第 5 步。

5.  将分类句柄和可写层数据发送到另一个函数以进行异步处理。 在该函数中，不在标注驱动程序的实现中执行剩余步骤[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)。

6.  调用[ **FwpsAcquireWritableLayerDataPointer0** ](https://msdn.microsoft.com/library/windows/hardware/ff550087)若要获取的可写数据结构所在的层[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)调用。 强制转换*writableLayerData* out 参数向结构对应于该层，要么[ **FWPS\_绑定\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551221)或[**FWPS\_CONNECT\_REQUEST0**](https://msdn.microsoft.com/library/windows/hardware/ff551231)。

    从 Windows 8 开始，如果您的标注驱动程序重定向到本地，则必须调用[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)填写**localRedirectHandle**的成员[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)结构以使工作代理。

7.  将任何特定于标注的上下文信息存储在专用上下文结构，如下面的示例中所示：

    ```C++
    redirectContext->classifyHandle = classifyHandle;
    redirectContext->connectRequest = connectRequest;
    redirectContext->classifyOut = *classifyOut; // deep copy
    // store original destination IP, port
    ```

8.  对层数据根据需要进行更改。

9.  调用[ **FwpsApplyModifiedLayerData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551137)要应用到数据所做的更改。 设置**FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS**标志，如果你想要在的另一个标注修改对数据进行进一步进行重新授权。

10. 调用[ **FwpsCompleteClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551150)以异步方式如下面的示例中所示完成分类操作：

    ```C++
    FwpsCompleteClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_PERMIT;
    classifyOut->rights |= FWPS_RIGHT_ACTION_WRITE;
    ```

11. 调用[ **FwpsReleaseClassifyHandle0** ](https://msdn.microsoft.com/library/windows/hardware/ff551208)释放在步骤 1 中获得的分类句柄。

### <a name="handling-connect-redirection-from-multiple-callouts"></a>处理从多个标注连接重定向

可能多个标注驱动程序将启动连接的同一个流重定向。 执行的标注连接重定向应注意的其他请求，并做出相应的响应。

**FWPS\_右\_操作\_编写**每当标注等待分类时，应设置标志。 用于测试应在标注**FWPS\_右\_操作\_编写**标志，用于检查在标注返回操作的权限。 如果未设置此标志，在标注仍会返回**FWP\_操作\_阻止**为了能否决操作**FWP\_操作\_允许**操作，返回上一个标注。

标注驱动程序在 Windows 8 和更高版本，必须通过使用查询 （请参阅如果标注驱动程序或另一个标注驱动程序是否修改它） 的连接的重定向状态[ **FwpsQueryConnectionRedirectState0**](https://msdn.microsoft.com/library/windows/hardware/hh439677)函数。 如果连接将重定向通过标注驱动程序，或者如果以前已被标注驱动程序重定向其，标注驱动程序不执行任何操作。 否则，它还应检查本地重定向，在下面的示例所示：

```C++
FwpsAcquireWritableLayerDataPointer(...,(PVOID*)&connectRequest), ...);
if(connectRequest->previousVersion->modifierFilterId != filterId)
{
    if(connectRequest->previousVersion->localRedirectHandle)
    {
        classifyOut->actionType = FWP_ACTION_PERMIT;
        classifyOut->rights &= FWPS_RIGHT_ACTION_WRITE;
        FwpsApplyModifiedLayerData(
                classifyHandle,
                (PVOID)connectRequest,
                FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS);
    }
}
```

如果连接到本地代理服务器，标注驱动程序不应尝试将其重定向。

使用的标注驱动程序连接重定向应注册在 ALE 授权连接层 (**FWPS\_层\_ALE\_身份验证\_CONNECT\_V4**或**FWPS\_层\_ALE\_身份验证\_CONNECT\_V6**)，并检查以下两个元数据值指示其中**FWP\_条件\_标志\_IS\_连接\_重定向**设置标志：

-   **FWPS\_元数据\_字段\_本地\_重定向\_目标\_PID**包含负责重定向流的进程的进程标识符。

-   **FWPS\_元数据\_字段\_原始\_目标**包含流的原始目标地址。

[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)结构包含一个名为成员**localRedirectTargetPID**。 对于任何环回连接重定向有效，将负责重定向流的进程的 PID，必须填充此字段。 这是在 ALE 授权引擎传递连接作为层的相同数据**FWPS\_元数据\_字段\_本地\_重定向\_目标\_ID**.

从 Windows 8 开始，代理服务需要颁发[ **SIO\_查询\_WFP\_连接\_重定向\_记录**](https://msdn.microsoft.com/library/windows/hardware/hh802473)并[ **SIO\_查询\_WFP\_连接\_重定向\_上下文**](https://msdn.microsoft.com/library/windows/hardware/hh802472) Ioctl，使用[**WSAIoctl**](https://msdn.microsoft.com/library/windows/desktop/ms741621)，针对代理服务的原始终结点。 此外， [ **SIO\_设置\_WFP\_连接\_重定向\_记录**](https://msdn.microsoft.com/library/windows/hardware/hh802474)必须颁发 IOCTL，使用**WSAIoctl**，新的 （代理） 套接字上。

## <a name="related-topics"></a>相关主题


[WFP 独立于版本的名称和目标的特定 Windows 版本](https://msdn.microsoft.com/library/windows/desktop/gg176678)

 

 






