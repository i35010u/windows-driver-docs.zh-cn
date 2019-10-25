---
title: 拨打电话
description: 拨打电话
ms.assetid: 295b3f6d-d53b-4030-b7e9-35ab7524d9aa
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，传出呼叫
- telephonic services WDK WAN，传出呼叫
- CoNDIS TAPI WDK 网络，传出呼叫
- 传出呼叫 WDK CoNDIS WAN
- 调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84556e2595d728716f31c6b9cbc6c475d8804797
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844130"
---
# <a name="making-outgoing-calls"></a>拨打电话





如果应用程序尝试发出传出调用，则必须先打开一行。 调用 TAPI **lineOpen**函数的应用程序会打开一条线。 若要在之前打开的行上放置电话服务呼叫，应用程序将调用 TAPI **lineMakeCall**函数，并传递指向特定目标地址的指针。 如果请求除默认调用设置参数外的任何参数，则应用程序还将传递指向 LINECALLPARAMS 结构的指针。 如果应用程序使用默认调用设置参数，则**lineMakeCall**将在 LINECALLPARAMS 结构中提供这些参数。 此结构的成员指定如何设置电话服务呼叫。

这些 TAPI 函数调用会导致 NDPROXY 驱动程序首先使用 CoNDIS WAN 微型端口驱动程序创建一个虚拟连接（VC），然后在 NDIS 结构中封装 TAPI 参数，以便发出传出调用。 微型端口驱动程序将使用这些 TAPI 参数设置传出呼叫。 下面介绍了如何连接、设置和发出传出呼叫：

-   NDPROXY 调用[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc) ，以启动通过微型端口驱动程序创建 VC。 NDPROXY 调用**NdisCoCreateVc**后，NDIS 会将调用管理器的*ProtocolCoCreateVc*函数作为同步操作调用，并将其集成到微型端口驱动程序中。 NDIS 传递到*ProtocolCoCreateVc*表示 VC 的句柄。 如果对**NdisCoCreateVc**的调用成功，NDIS 将填充并返回 VC 句柄。 *ProtocolCoCreateVc*执行动态资源和结构的任何必要分配，小型端口调用管理器（MCM）驱动程序需要在以后激活的 VC 上执行后续操作。 此类资源包括但不限于内存缓冲区、数据结构、事件以及其他此类类似资源。

-   NDPROXY 指定 CO\_AF 中传出呼叫的 TAPI 参数[ **\_tapi\_使\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545373(v=vs.85))结构。 NDPROXY 用 TAPI **lineMakeCall**函数中传递的以下信息填充此结构的成员：
    -   **DestAddress**成员中的目标地址
    -   **UlLineID**成员中的开放行标识符
    -   **LINECALLPARAMS**成员中的 LINECALLPARAMS 结构
-   NDPROXY 覆盖了 CO\_AF\_TAPI\_使\_调用\_[**参数结构的**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85)) **parameters**成员的参数结构，并设置 co 的**Length**成员将特定\_参数\_到 CO\_AF\_TAPI 大小\_使\_调用\_参数。

-   NDPROXY 将\_特定\_参数结构设置为[**co\_MEDIA\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))结构的**MediaSpecific**成员。

-   NDPROXY 将指向 co\_MEDIA\_参数结构的指针设置为[**co\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构的**MediaParameters**成员。

-   NDPROXY 封装 TAPI 参数后，NDPROXY 将调用[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)函数以启动传出调用。 在此函数调用中，NDPROXY 将指针传递到实心 CO\_调用\_参数结构。 NDIS 反过来调用 CoNDIS WAN 微型端口驱动程序的调用管理器的[**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)函数。 微型端口驱动程序只应检查 CO\_AF\_TAPI\_使\_调用\_参数结构嵌入在共同\_调用\_参数中。 在这种情况下，任何其他调用参数都是有意义的。 如果微型端口驱动程序随后激活了用于传出调用的 VC，微型端口驱动程序将调用[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)函数，并将一个指针传递到实心 CO\_调用\_参数。

-   当微型端口驱动程序与网络协商以建立 VC 的电话呼叫参数并为这些调用参数设置 NIC 后，微型端口驱动程序将调用[**NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmakecallcomplete)函数，以指示它已准备就绪，可以进行在 VC 上传输数据。 在此调用中，微型端口驱动程序必须将句柄传递给 VC，并对电话呼叫参数所做的修改。

-   微型端口驱动程序必须修改 CO\_调用\_参数结构的**CallMgrParameters**成员，以指定传输数据包的服务质量（QoS），如带宽。 若要设置此**CallMgrParameters**成员，微型端口驱动程序将填充[**CO\_调用的成员\_MANAGER\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构，并将此结构指向**CallMgrParameters**。 例如，若要确定 VC 的传输和接收速度（以每秒字节数为单位），微型端口驱动程序必须设置联合\_调用\_管理器的**传输**和**接收**成员的**PeakBandwidth**成员\_PARAMETERS. **传输**和**接收**成员是 FLOWSPEC 结构。 有关 FLOWSPEC 结构的详细信息，请参阅 Microsoft Windows SDK。

-   如果微型端口驱动程序已修改电话服务调用参数，则它必须设置 CO\_调用中的**Flags**成员\_参数结构，并\_更改调用\_参数。 由于微型端口驱动程序发出的**NdisMCmMakeCallComplete**调用，NDIS 调用 NDPROXY 的*ProtocolClMakeCallComplete*函数来完成使用**NdisClMakeCall**启动的异步操作。

-   当微型端口驱动程序成功完成传出调用后，NDPROXY 会通知 TAPI 应用程序呼叫已连接。 然后，此 TAPI 应用程序调用 TAPI **lineGetID**函数，通知 NDPROXY 查找相应的 CoNDIS 客户端。 在此**lineGetID**调用中，tapi 应用程序为特定 TAPI 设备类提供一个字符串，应用程序需要一个句柄。 NDPROXY 使用此字符串来查找以前为特定 TAPI 设备类注册了 SAP 的 CoNDIS 客户端。 如果 CoNDIS 客户端为 NDISWAN，则字符串为 NDIS。 如果 NDPROXY 找到一个字符串与 TAPI 应用程序传递的字符串相匹配的 SAP，则 NDPROXY 会调用[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)来设置一个带 NDISWAN 的连接终结点，在该终结点上可调度发出的传出调用通知。 NDIS 反过来调用 NDISWAN 的*ProtocolCoCreateVc*函数并传递表示 VC 的句柄。

-   NDPROXY 通过 NDISWAN 设置连接终结点后，它将调用[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)函数以通知 NDISWAN 有关传出调用的信息。 在此调用中，NDPROXY 将封装的 CO\_AF\_TAPI\_使\_调用包含传出调用参数的\_参数结构。 NDIS 反过来调用 NDISWAN 的*ProtocolClIncomingCall*函数，其中 NDISWAN 接受或拒绝请求的连接。 如果 NDISWAN 更改了传递给它的调用参数，则它必须设置 CO\_调用中的**Flags**成员\_参数结构的调用\_参数\_更改。

-   在决定是否接受连接之后以及在可能更改调用参数之后，NDISWAN 会调用[**NdisClIncomingCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete)函数。 NDIS 又调用微型端口驱动程序的*ProtocolCmIncomingCallComplete*函数。 根据 NDISWAN 是否接受传出呼叫以及微型端口驱动程序是接受还是拒绝 NDISWAN 对调用参数的建议更改，微型端口驱动程序会调用[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected)或[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall)函数。 **NdisCmDispatchCallConnected**将通知 NDISWAN，可从 NDPROXY 为传出调用创建的 VC 开始数据传输。 **NdisCmDispatchIncomingCloseCall**通知 NDISWAN 和 NDPROXY，以关闭建议的传出呼叫。

-   NDISWAN 接受传出调用后，NDPROXY 调用[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)函数以检索用于标识 VC 的 NDISWAN 上下文的字符串。 NDPROXY 将此字符串传递回 TAPI 应用程序。 TAPI 应用程序使用此 VC 上下文字符串来完成对**lineGetID**的调用。

 

 





