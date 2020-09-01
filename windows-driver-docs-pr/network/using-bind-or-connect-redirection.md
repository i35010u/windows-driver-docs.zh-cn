---
title: 使用绑定或连接重定向
description: 使用绑定或连接重定向
ms.assetid: 6b27a9ad-53e9-4e80-bf03-79665f8a82a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6734763567486e8589be626962f56bbb28e7be9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217241"
---
# <a name="using-bind-or-connect-redirection"></a>使用绑定或连接重定向


Windows 筛选平台的连接/绑定重定向功能 (WFP) 使应用程序层强制 (ALE) 标注驱动程序检查和（如果需要）重定向连接。

此功能在 Windows 7 及更高版本中可用。

**注意**   \_ [WFP 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618934)中的 ClassifyFunctions ProxyCallouts 模块包含的代码演示了连接/绑定重定向。

 

WFP 连接重定向标注可重定向应用程序的连接请求，使应用程序可以连接到代理服务而不是原始目标。 代理服务有两个套接字：一个用于重定向的原始连接，另一个用于新代理的出站连接。

WFP 重定向记录是不透明数据的缓冲区，WFP 必须在 FWPM 层的出站代理连接上设置，这是在 ** \_ 层 ale authentication authentication \_ \_ \_ Connect \_ 重定向 \_ V4** 和 **FWPM \_ 层 \_ ale \_ \_ \_ \_ ** authentication authentication

由于可以使用绑定重定向，因此不需要在连接重定向中支持本地地址和端口修改。 不支持在连接重定向过程中更改本地地址和端口。

### <a name="layers-used-for-redirection"></a>用于重定向的层

可以通过以下层上的标注驱动程序执行重定向： "重定向层"：

-   FWPM \_ 层 \_ ale \_ 绑定 \_ 重定向 \_ v4 (FWPS \_ 层 \_ ale \_ 绑定 \_ 重定向 \_ v4) 

-   FWPM \_ 层 \_ ale \_ 绑定 \_ 重定向 \_ v6 (FWPS \_ 层 \_ ale \_ 绑定 \_ 重定向 \_ v6) 

-   FWPM \_ 层 \_ ale \_ connect \_ 重定向 \_ v4 (FWPS \_ 层 \_ ale \_ connect \_ 重定向 \_ v4) 

-   FWPM \_ 层 \_ ale \_ connect \_ 重定向 \_ v6 (FWPS \_ 层 \_ ale \_ connect \_ 重定向 \_ v6) 

执行重定向的层决定了更改的影响。 连接层的更改仅影响正在连接的流。 绑定层上的更改会影响使用该套接字的所有连接。

重定向层仅适用于 windows 7 和更高版本的 Windows。 支持这些层分类的标注驱动程序必须使用 [**FwpsCalloutRegister1**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1) 或更高版本注册，而不是使用较旧的 [**FwpsCalloutRegister0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0) 函数。

> [!IMPORTANT]
> 重定向不可用于所有类型的网络流量。 以下列表显示了重定向支持的数据包类型：
> - TCP
> - UDP
> - 不带标头包含选项的原始 UDPv4
> - 原始 ICMP

### <a name="performing-redirection"></a>执行重定向

若要重定向连接，标注驱动程序必须获取 TCP 4 元组信息的可写副本，并根据需要对其进行更改，并应用所做的更改。 提供了一组新函数，用于获取可写层数据，并通过引擎应用该数据。 标注驱动程序可以选择在 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) 函数中以内联方式进行更改，也可以在另一个函数中异步更改。

实现重定向的标注驱动程序必须使用 [*classifyFn1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn1) 或更高版本，而不是 [*classifyFn0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 作为其分类标注函数。 若要使用 *classifyFn1* 或更高版本，必须通过调用 [**FwpsCalloutRegister1**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1) 或更高版本，而不是旧的 [**FwpsCalloutRegister0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister0)来注册标注。

若要执行重定向，必须在其 [classifyFn](/windows-hardware/drivers/ddi/_netvista/)实现中执行以下步骤：

1.  调用 [**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0) 以获取可用于重定向 TCP 连接的句柄。 应缓存此句柄并将其用于所有重定向。 对于 Windows 7 和更早版本，将忽略此步骤 (。 ) 

2.  在 Windows 8 及更高版本中，必须使用标注驱动程序中的 [**FwpsQueryConnectionRedirectState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0) 函数来查询连接的重定向状态。 必须执行此操作以防止无限重定向。

3.  调用 [**FwpsAcquireClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0) 以获取将用于后续函数调用的句柄。

4.  调用 [**FwpsAcquireWritableLayerDataPointer0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0) 可获取调用 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) 的层的可写数据结构。 将 *writableLayerData* out 参数强制转换为与该层对应的结构， [**FWPS \_ 绑定 \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0) 或 [**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)。

    从 Windows 8 开始，如果标注驱动程序重定向到本地服务，则必须调用[**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)来填充[**FWPS \_ 连接 \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)结构的**localRedirectHandle**成员，才能使本地代理正常工作。

5.  根据需要对层数据进行更改：

    1.  将原始目标保存在本地重定向上下文中，如以下示例中所示：

        ```C++
        FWPS_CONNECT_REQUEST* connectRequest = redirectContext->connectRequest;
        // Replace "..." with your own redirect context size
        connectRequest->localRedirectContextSize = ...;
        // Store original destination IP/Port information in the localRedirectContext member
        connectRequest->localRedirectContext =    ExAllocatePoolWithTag(…);
        ```

    2.  修改远程地址，如以下示例中所示：

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

    3.  如果你的标注驱动程序重定向到本地服务，则它应在[**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)结构的**localRedirectTargetPID**成员中设置本地代理 PID。
    4.  如果你的标注驱动程序重定向到本地服务，则它应设置 FwpsRedirectHandleCreate0 在 FWPS **localRedirectHandle** \_ CONNECT REQUEST0 结构的 localRedirectHandle 成员中返回的重定向句柄 \_ 。

6.  调用 [**FwpsApplyModifiedLayerData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0) 以应用对数据所做的更改。

7.  在代理服务中 (可能在用户模式下或内核模式) ，你应该查询重定向记录和上下文，如以下示例中所示：

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

8.  在代理服务中 (可能处于用户模式或内核模式) ，应在代理连接套接字上设置重定向记录，如以下示例中所示，用于创建新的出站套接字：

    ```C++
    proxySock = WSASocket(…);
    result = WSAIoctl(
                 proxySock,
                 SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS,
                 redirectRecords, …);
    ```

9.  调用 [**FwpsReleaseClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0) ，以释放在步骤2中获取的分类句柄。

10. 调用 [**FwpsRedirectHandleDestroy0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0) 以销毁在步骤1中获取的句柄。

若要以异步方式执行重定向，标注驱动程序必须执行以下步骤：

1.  调用 [**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0) 以获取可用于重定向 TCP 连接的句柄。 对于 Windows 7 和更早版本，将忽略此步骤 (。 ) 

2.  在 Windows 8 及更高版本中，必须使用标注驱动程序中的 [**FwpsQueryConnectionRedirectState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0) 函数来查询连接的重定向状态。

3.  调用 [**FwpsAcquireClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0) 以获取将用于后续函数调用的句柄。 此步骤和步骤2和步骤3是在标注驱动程序的 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) callout 函数中执行的。

4.  调用 [**FwpsPendClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0) ，将分类置于挂起状态，如以下示例中所示：

    ```C++
    FwpsPendClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_BLOCK;
    classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    ```

> [!NOTE]
> 如果你面向的是 Windows 7，则必须在单独的辅助角色函数中执行以下步骤。 如果你面向的是 Windows 8 或更高版本，则可以从 *classifyFn* 中执行异步重定向的所有步骤，并忽略步骤5。

5.  将分类句柄和可写层数据发送到另一个函数以进行异步处理。 其余步骤在该函数中执行，而不是在 [classifyFn](/windows-hardware/drivers/ddi/_netvista/)的标注驱动程序实现中执行。

6.  调用 [**FwpsAcquireWritableLayerDataPointer0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0) 可获取调用 [classifyFn](/windows-hardware/drivers/ddi/_netvista/) 的层的可写数据结构。 将 *writableLayerData* out 参数强制转换为与该层对应的结构， [**FWPS \_ 绑定 \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0) 或 [**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)。

    从 Windows 8 开始，如果标注驱动程序在本地重定向，则必须调用[**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)来填充[**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)结构的**localRedirectHandle**成员，以使代理工作。

7.  在私有上下文结构中存储任何标注特定的上下文信息，如以下示例中所示：

    ```C++
    redirectContext->classifyHandle = classifyHandle;
    redirectContext->connectRequest = connectRequest;
    redirectContext->classifyOut = *classifyOut; // deep copy
    // store original destination IP, port
    ```

8.  根据需要对层数据进行更改。

9.  调用 [**FwpsApplyModifiedLayerData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0) 以应用对数据所做的更改。 如果希望在其他标注进一步修改数据时重新获得授权，请设置 **FWPS_CLASSIFY_FLAG_REAUTHORIZE_IF_MODIFIED_BY_OTHERS** 标志。

10. 如以下示例中所示，通过异步方式调用 [**FwpsCompleteClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0) 来完成分类操作：

    ```C++
    FwpsCompleteClassify(
            redirectContext->classifyHandle,
            0,
            &redirectContext->classifyOut);
    classifyOut->actionType = FWP_ACTION_PERMIT;
    classifyOut->rights |= FWPS_RIGHT_ACTION_WRITE;
    ```

11. 调用 [**FwpsReleaseClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0) ，以释放在步骤1中获取的分类句柄。

### <a name="handling-connect-redirection-from-multiple-callouts"></a>处理来自多个标注的 Connect 重定向

多个标注驱动程序可能会为同一流启动连接重定向。 执行连接重定向的标注应知道其他请求，并做出相应的响应。

只要标注 pends 分类，就应设置 **FWPS \_ 权限 \_ 操作 \_ 写入** 标志。 你的标注应测试 **FWPS \_ 权限 \_ 操作 \_ 写入** 标志，以检查标注的权限以返回一个操作。 如果未设置此标志，则标注仍可返回 **.Fwp \_ 操作 \_ 阻止** 操作，以便否决先前标注返回的 **允许的 .fwp \_ 操作 \_ 允许** 操作。

在 Windows 8 及更高版本中，标注驱动程序必须查询连接 (的重定向状态，以查看标注驱动程序或其他标注驱动程序是否已使用 [**FwpsQueryConnectionRedirectState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0) 函数对其进行了修改) 。 如果连接由您的标注驱动程序重定向，或者它以前被您的标注驱动程序重定向，则标注驱动程序应不执行任何操作。 否则，还应检查本地重定向，如以下示例中所示：

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

如果连接到本地代理，则标注驱动程序不应尝试重定向。

使用 connect 重定向的标注驱动程序应在 ALE 授权连接层上注册 (**FWPS \_ 层 \_ ale authentication \_ \_ connect \_ V4** 或 **FWPS \_ 层 \_ ale authentication connect) \_ \_ \_ V6** ，并检查以下两个元数据值，以查找在其中设置了 " **.fwp \_ 条件 \_ 标志 \_ 是 \_ 连接 \_ 重定向** 标志" 的指示：

-   **FWPS \_元数据 \_ 字段 \_ 本地 \_ 重定向 \_ 目标 \_ PID** 包含负责重定向流的进程的进程标识符。

-   **FWPS \_元数据 \_ 字段 \_ 原始 \_ 目标** 包含流的原始目标地址。

[**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)结构包含名为**localRedirectTargetPID**的成员。 要使任何环回 connect 重定向有效，必须用负责重定向流的进程的 PID 来填充此字段。 此数据与引擎在 ALE 授权连接层上传递的数据相同， **FWPS \_ 元数据 \_ 字段 \_ 本地 \_ 重定向 \_ 目标 \_ ID**。

从 Windows 8 开始，代理服务需要对代理服务的原始终结点发出 [**SIO \_ 查询 \_ wfp \_ 连接 \_ 重定向 \_ 记录**](./sio-query-wfp-connection-redirect-records.md) 和 [**SIO \_ 查询 \_ wfp \_ 连接 \_ 重定向 \_ 上下文**](./sio-query-wfp-connection-redirect-context.md) IOCTLs，使用 [**WSAIoctl**](/windows/desktop/api/winsock2/nf-winsock2-wsaioctl)。 此外，必须在新的 (代理) 套接字上，使用**WSAIoctl**对[**SIO \_ SET \_ WFP \_ 连接 \_ 重定向 \_ 记录**](./sio-set-wfp-connection-redirect-records.md)IOCTL 发出。

## <a name="related-topics"></a>相关主题


[与版本无关的 WFP 名称并面向特定版本的 Windows](/windows/desktop/FWP/wfp-version-independent-names-and-targeting-specific-versions-of-windows)

 

