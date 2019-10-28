---
title: 接受来电
description: 接受来电
ms.assetid: bca837dc-b3de-4aca-9fc2-aed2faab1377
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，传入呼叫
- telephonic services WDK WAN，传入呼叫
- CoNDIS TAPI WDK 网络，传入呼叫
- NDPROXY WDK 网络，传入呼叫
- 呼入 CoNDIS WAN
- 调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d8b041ce1495648f6a2512acc9c456c2e9759e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838256"
---
# <a name="accepting-incoming-calls"></a>接受来电





在应用程序可以接受传入呼叫之前，必须先打开一行。 调用 TAPI **lineOpen**函数的应用程序会打开一条线。 此 TAPI 功能调用会导致基础驱动程序在 NDIS 结构中封装 TAPI 参数，以便准备接收传入呼叫。 CoNDIS WAN 微型端口驱动程序收到传入呼叫后，微型端口驱动程序必须先使用 NDPROXY 驱动程序创建一个虚拟连接（VC），然后通知 NDPROXY 传入呼叫。 NDPROXY 反过来会通过 TAPI 通知应用程序。 以下列表描述了如何设置、连接和进行传入呼叫：

-   NDPROXY 指定 CO\_AF 中传入连接的 TAPI 参数[ **\_tapi\_SAP**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545376(v=vs.85))结构。 NDPROXY 用 TAPI **lineOpen**函数中传递的以下信息填充此结构的成员：
    -   **UlLineID**成员中的换行标识符
    -   **UlAddressID**成员中传入连接的地址
    -   **UlMediaModes**成员中传入连接的信息流的媒体模式
-   NDPROXY 覆盖了共同[ **\_sap**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构的**sap**成员上的 CO\_AF\_TAPI\_sap 结构，并将 Co\_sap 的**SapLength**成员设置为 co\_AF\_TAPI 的大小\_SAP。 NDPROXY 还必须将 CO\_SAP 的**SapType**成员设置为 AF\_TAPI\_SAP\_类型。

-   NDPROXY 封装 TAPI 参数后，NDPROXY 会调用[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)函数，使其能够接收传入调用。 在此函数调用中，NDPROXY 将一个指针传递到实心 CO\_SAP 结构，该结构指定 NDPROXY 可在其上接收传入呼叫的服务访问点（SAP）。 NDIS 将 CO\_SAP 结构转发到 CoNDIS WAN 微型端口调用管理器（MCM）驱动程序的*ProtocolCmRegisterSap*函数。 如有必要， *ProtocolCmRegisterSap*会与网络控制设备或其他特定于介质的代理通信，以便在网络上为 NDPROXY 注册 SAP。 小型端口驱动程序注册了 SAP 后，可接受定向到该 SAP 的传入呼叫提议。

-   CoNDIS WAN 微型端口驱动程序通过从网络发出消息通知传入呼叫。 通过这些信号消息，微型端口驱动程序会提取调用的调用参数，包括传入调用的目标 SAP。

-   在指示对 NDPROXY 的传入调用之前，微型端口驱动程序调用[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)函数来启动使用 NDPROXY 创建 VC。 NDPROXY 分配和初始化 VC 所需的资源，并将句柄存储到 VC。

-   CoNDIS WAN 微型端口驱动程序设置 CO\_AF 中传入呼叫的 TAPI 参数[ **\_tapi\_传入\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545372(v=vs.85))结构。 微型端口驱动程序用从信号消息中提取的以下信息填充此结构的成员：
    -   **UlLineID**成员中的行标识符
    -   **UlAddressID**成员中传入调用的地址
    -   \_的 TAPI\_标志\_**ulFlags**成员中的传入\_调用位。 **UlFlags**的所有其他位均保留，并且必须设置为0。
    -   **LineCallInfo**成员中的 LINECALLPARAMS 结构。 LINECALLPARAMS 的成员为传入呼叫指定 TAPI 调用参数。
-   微型端口驱动程序[**覆盖 co\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85)) AF\_TAPI\_传入\_调用\_参数结构的**参数**成员上的参数，并设置的**长度**成员将特定\_参数\_到 CO\_AF 的大小\_TAPI\_传入\_调用\_参数。

-   微型端口驱动程序将 CO\_特定\_参数结构设置为[**co\_MEDIA\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))结构的**MediaSpecific**成员。

-   微型端口驱动程序将指向 CO\_MEDIA\_参数结构的指针设置为[**co\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构的**MediaParameters**成员。

-   微型端口驱动程序还必须将 CO\_调用的**CallMgrParameters**成员设置\_PARAMETERS 结构，以指定传输数据包的服务质量（QoS），如带宽。 若要设置此**CallMgrParameters**成员，微型端口驱动程序将填充[**CO\_调用的成员\_MANAGER\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构，并将此结构指向**CallMgrParameters**。 例如，若要确定 VC 的传输和接收速度（以每秒字节数为单位），微型端口驱动程序必须设置联合\_调用\_管理器的**传输**和**接收**成员的**PeakBandwidth**成员\_PARAMETERS. **传输**和**接收**成员是 FLOWSPEC 结构。 有关 FLOWSPEC 结构的详细信息，请参阅 Microsoft Windows SDK。

-   在微型端口驱动程序封装 TAPI 参数并填充 CO\_调用\_MANAGER\_参数的**CallMgrParameters**成员后，它将调用[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)函数以指示对的传入调用NDPROXY. 在此调用中，微型端口驱动程序将传递以下内容：
    -   用于标识传入呼叫的目标 SAP 的句柄
    -   用于标识传入调用的 VC 的句柄
    -   指向已填充 CO\_调用的指针\_参数结构
-   NDPROXY 返回\_挂起到微型端口驱动程序的 NDIS\_状态，以便 NDPROXY 可以异步完成**NdisMCmDispatchIncomingCall** 。

-   TAPI 应用程序通过**lineAnswer**函数应答传入调用后，NDPROXY 将调用[**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)函数。 NDIS 又调用微型端口驱动程序的*ProtocolCmIncomingCallComplete*函数。 如果 NDPROXY 返回 NDIS\_状态\_成功代码，则表示接受调用参数。 如果 NDPROXY 发现调用参数不可接受，则它可以通过设置 CO\_调用中的**Flags**成员\_参数结构来调用\_参数\_更改，并通过提供修订来请求更改调用参数调用参数。 如果 NDPROXY 接受传入呼叫，微型端口驱动程序应发送信号消息，向调用方指明调用已被接受。 否则，微型端口驱动程序应发送信号消息，指示调用已被拒绝。 如果 NDPROXY 请求在调用参数中进行更改，微型端口驱动程序将发送信号消息，请求在调用参数中进行更改。

-   微型端口驱动程序激活用 NDPROXY 创建的微型端口驱动程序的 VC，还必须调用[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)函数来通知 NDPROXY 微型端口驱动程序已准备好在 VC 上传输数据包。

-   如果 NDPROXY 拒绝呼叫，微型端口驱动程序会调用[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)函数来停用用于为传入调用创建微型端口驱动程序的 VC。 禁用 VC 后，微型端口驱动程序将调用[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)函数来删除 vc。

-   根据 NDPROXY 是否接受传入呼叫以及是否已成功建立端到端连接，微型端口驱动程序将调用[**NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchcallconnected)或[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall)函数. 请注意，如果远程调用实体 t) 调用，它将发送信号消息，指示未成功建立端到端连接。 **NdisMCmDispatchCallConnected**通知 NDPROXY，数据传输可以在 VC 上开始，该 VC 驱动程序已为传入调用创建并激活。 **NdisMCmDispatchIncomingCloseCall**通知 NDPROXY 关闭传入呼叫。

-   如果定向到 NDPROXY 以拆下传入调用，它将调用[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)函数，以确认它既不会尝试发送，也不希望在 VC 上接收数据。 NDIS 又调用微型端口驱动程序的*ProtocolCmCloseCall*函数。 然后，小型端口驱动程序会调用**NdisMCmDeactivateVc**函数来停用 VC。 禁用 VC 后，微型端口驱动程序将调用**NdisMCmDeleteVc**函数来删除 vc。

-   在 TAPI 应用程序接受传入呼叫并且 NDPROXY 通知应用程序呼叫已连接后，应用程序将调用 TAPI **lineGetID**函数来通知 NDPROXY 查找相应的 CoNDIS 客户端。 在此**lineGetID**调用中，tapi 应用程序为特定 TAPI 设备类提供一个字符串，应用程序需要一个句柄。 NDPROXY 使用此字符串来查找以前为特定 TAPI 设备类注册了 SAP 的 CoNDIS 客户端。 如果 CoNDIS 客户端为 NDISWAN，则字符串为 NDIS。 如果 NDPROXY 找到一个字符串与 TAPI 应用程序传递的字符串相匹配的 SAP，则 NDPROXY 会调用**NdisMCmCreateVc**来设置一个具有 NDISWAN 的连接终结点，在该终结点上可调度传入调用的通知。 NDIS 反过来调用 NDISWAN 的*ProtocolCoCreateVc*函数并传递表示 VC 的句柄。

-   NDPROXY 通过 NDISWAN 设置连接终结点后，它将调用[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)函数以通知 NDISWAN 有关传入调用的信息。 在此调用中，NDPROXY 将封装的 CO\_AF\_TAPI\_传入\_调用\_包含传入调用参数的参数结构。 NDIS 反过来调用 NDISWAN 的*ProtocolClIncomingCall*函数，其中 NDISWAN 接受或拒绝请求的连接。

-   在决定是否接受连接之后以及在可能更改调用参数之后，NDISWAN 会调用**NdisClIncomingCallComplete**函数。 NDIS 又调用微型端口驱动程序的*ProtocolCmIncomingCallComplete*函数。 根据 NDISWAN 是否接受传入呼叫，以及微型端口驱动程序是接受还是拒绝 NDISWAN 对调用参数的建议更改，微型端口驱动程序调用**NdisCmDispatchCallConnected**或**NdisCmDispatchIncomingCloseCall**函数。 **NdisCmDispatchCallConnected**通知 NDISWAN，数据传输可以在 VC 上开始，该 VC 是为传入调用创建的微型端口驱动程序。 **NdisCmDispatchIncomingCloseCall**通知 NDISWAN 和 NDPROXY 解除传入呼叫。

-   NDISWAN 接受传入调用后，NDPROXY 将调用[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)函数以检索用于标识 VC 的 NDISWAN 上下文的字符串。 NDPROXY 将此字符串传递回 TAPI 应用程序。 TAPI 应用程序使用此 VC 上下文字符串来完成对**lineGetID**的调用。

 

 





