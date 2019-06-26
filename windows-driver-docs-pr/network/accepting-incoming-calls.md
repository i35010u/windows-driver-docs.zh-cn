---
title: 接受来电
description: 接受来电
ms.assetid: bca837dc-b3de-4aca-9fc2-aed2faab1377
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络连接、 传入调用
- WDK WAN，传入呼叫的电话服务
- CoNDIS TAPI WDK 网络连接、 传入调用
- NDPROXY WDK 网络连接、 传入调用
- WDK 的 CoNDIS WAN 的传入呼叫
- 调用 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a90c92c71a2b362cec0f11be80b0c46889c4dbb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378697"
---
# <a name="accepting-incoming-calls"></a>接受来电





应用程序可接受的传入呼叫之前，它首先必须具有打开的行。 由于调用 TAPI 的应用程序打开一个行**lineOpen**函数。 此 TAPI 函数调用会导致基础驱动程序为了准备接收的传入呼叫封装 TAPI NDIS 结构中的参数。 WAN 的 CoNDIS 微型端口驱动程序收到的传入呼叫后，微型端口驱动程序必须首先通过 NDPROXY 驱动程序创建的虚拟连接 (VC)，，然后通知 NDPROXY 传入呼叫。 NDPROXY 反过来会通知应用程序通过 TAPI。 以下列表描述传入呼叫的设置方式，连接，然后进行：

-   NDPROXY TAPI 为指定参数中传入的连接[**共同\_AF\_TAPI\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545376(v=vs.85))结构。 NDPROXY 填充此结构的成员使用以下信息在 TAPI 中传递**lineOpen**函数：
    -   在打开行标识符**ulLineID**成员
    -   中的传入连接的地址**ulAddressID**成员
    -   媒体模式中的传入连接的信息流**ulMediaModes**成员
-   NDPROXY 叠加产生的 CO\_AF\_TAPI\_上的 SAP 结构**Sap**隶属[**共同\_SAP** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构并设置**SapLength**成员产生的 CO\_产生的 CO 大小 SAP\_AF\_TAPI\_SAP。 此外必须设置 NDPROXY **SapType**成员产生的 CO\_SAP 再到 AF\_TAPI\_SAP\_类型。

-   一旦 NDPROXY 封装 TAPI 参数，调用 NDPROXY [ **NdisClRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap)函数来准备好接收传入的呼叫将本身。 在此函数调用中，NDPROXY 将指针传递到已填充共同\_SAP 结构，它指定 NDPROXY 可以接收传入的呼叫服务访问点 (SAP)。 NDIS 转发产生的 CO\_SAP 结构*ProtocolCmRegisterSap* CoNDIS WAN 小型端口调用管理器 (MCM) 驱动程序的函数。 *ProtocolCmRegisterSap*与网络控制设备或其他特定于媒体的代理，在必要时，若要注册 NDPROXY 网络上的 SAP 通信。 微型端口驱动程序已注册 SAP 后，它可以接受定向到该 SAP 的传入调用产品/服务。

-   CoNDIS WAN 的微型端口驱动程序是向你发出警报的传入呼叫到信号消息从网络。 从这些信号消息，微型端口驱动程序提取的调用中，包括的 SAP 向其发送传入调用的调用参数。

-   之前，该值指示对 NDPROXY 的传入呼叫，微型端口驱动程序调用[ **NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)函数来启动与 NDPROXY VC 的创建。 NDPROXY 分配和初始化所需的 VC 资源并将存储到 VC 句柄。

-   WAN 的 CoNDIS 微型端口驱动程序设置中的传入呼叫的 TAPI 参数[**共同\_AF\_TAPI\_传入\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545372(v=vs.85))结构。 微型端口驱动程序填充此结构的成员从信号消息中提取的以下信息：
    -   行中的标识符**ulLineID**成员
    -   中的传入调用的地址**ulAddressID**成员
    -   CO\_TAPI\_标志\_传入\_调用中位**ulFlags**成员。 所有其他位**ulFlags**是保留字符，必须设置为 0。
    -   在结构 LINECALLPARAMS **LineCallInfo**成员。 LINECALLPARAMS 的成员指定的传入呼叫的 TAPI 调用参数。
-   微型端口驱动程序覆盖共同\_AF\_TAPI\_传入\_调用\_上的参数**参数**隶属[**共同\_特定\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))结构和集**长度**成员产生的 CO\_特定\_产生的 CO 大小参数\_AF\_TAPI\_传入\_调用\_参数。

-   微型端口驱动程序设置产生的 CO\_特定\_参数结构**MediaSpecific**的成员[**共同\_媒体\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545388(v=vs.85))结构。

-   微型端口驱动程序将指针设置为产生的 CO\_媒体\_参数结构**MediaParameters**的成员[**共同\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))结构。

-   微型端口驱动程序还必须设置**CallMgrParameters**成员产生的 CO\_调用\_参数结构，以指定的服务质量 (QoS 传输数据包，带宽等)。 若要设置此**CallMgrParameters**成员，微型端口驱动程序填充的成员[**共同\_调用\_MANAGER\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构和点到此结构**CallMgrParameters**。 例如，若要确定传输并以字节为单位的 VC 每秒接收的速度，微型端口驱动程序必须设置**PeakBandwidth**的成员**传输**和**接收**成员产生的 CO\_调用\_MANAGER\_参数。 **传输**并**接收**成员是流程规格结构。 有关流程规格结构的详细信息，请参阅 Microsoft Windows SDK。

-   后微型端口驱动程序封装 TAPI 参数和填充**CallMgrParameters**成员产生的 CO\_调用\_MANAGER\_参数，它将调用[ **NdisMCmDispatchIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall)函数来指示对 NDPROXY 传入呼叫。 在此调用中，通过以下微型端口驱动程序：
    -   标识向其发送传入的调用将 SAP 句柄
    -   标识用于传入呼叫 VC 句柄
    -   指向已填充共同\_调用\_参数结构
-   NDPROXY 返回 NDIS\_状态\_微型端口驱动程序因此 NDPROXY 可以完成的 PENDING **NdisMCmDispatchIncomingCall**以异步方式。

-   TAPI 后应用程序应答传入呼叫与**lineAnswer**函数，将调用 NDPROXY [ **NdisClIncomingCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclincomingcallcomplete)函数。 NDIS 反过来调用微型端口驱动程序*ProtocolCmIncomingCallComplete*函数。 如果 NDPROXY 返回 NDIS\_状态\_成功代码，它表示调用参数接受。 如果 NDPROXY 找到调用参数不可接受，它可以通过设置请求的调用参数中的更改**标志**成员中产生的 CO\_调用\_调用的参数结构\_参数\_已更改并通过提供修改后的调用的参数。 如果 NDPROXY 接受传入呼叫，微型端口驱动程序应发送信号消息来指示发给调用实体调用已被接受。 否则，微型端口驱动程序应将发送信号消息来指示调用已被拒绝。 如果 NDPROXY 请求在调用参数中，微型端口驱动程序发送信号消息，以请求更改调用参数中的更改。

-   微型端口驱动程序将激活的微型端口驱动程序使用 NDPROXY 创建，并且还必须调用 VC [ **NdisMCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)函数，以通知 NDPROXY 微型端口驱动程序已准备好传输VC 的数据包。

-   如果 NDPROXY 拒绝呼叫，微型端口驱动程序会调用[ **NdisMCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc)要停用 VC 微型端口驱动程序创建传入调用的函数。 VC 停用后，微型端口驱动程序会调用[ **NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc)函数来删除 VC。

-   具体取决于是否 NDPROXY 接受传入呼叫和是否已成功建立端到端连接，微型端口驱动程序拨打[ **NdisMCmDispatchCallConnected** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchcallconnected)或[ **NdisMCmDispatchIncomingCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingclosecall)函数。 请注意，如果远程调用实体撕裂的调用，它将发送信号消息以指示不已成功建立端到端连接。 **NdisMCmDispatchCallConnected**通知 NDPROXY VC 微型端口驱动程序创建并激活的传入呼叫可以开始数据传输。 **NdisMCmDispatchIncomingCloseCall**通知 NDPROXY 关闭传入呼叫。

-   如果 NDPROXY 重定向，以关闭传入调用，则会调用[ **NdisClCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall)函数以确认，它将既不尝试发送，也不会收到 VC 上的数据。 NDIS 反过来调用微型端口驱动程序*ProtocolCmCloseCall*函数。 然后调用微型端口驱动程序**NdisMCmDeactivateVc**函数来停用 VC。 VC 停用后，微型端口驱动程序会调用**NdisMCmDeleteVc**函数来删除 VC。

-   在应用程序的 TAPI 应用程序接受传入呼叫并 NDPROXY 通知应用程序连接呼叫后，调用 TAPI **lineGetID**函数来通知 NDPROXY 来查找相应的 CoNDIS 客户端。 在此**lineGetID**调用，TAPI 应用程序提供特定的 TAPI 设备类向其应用程序需要一个句柄的字符串。 NDPROXY 使用此字符串来找到以前注册的特定 TAPI 设备类的 SAP 的 CoNDIS 客户端。 如果 NDISWAN CoNDIS 客户端，则该字符串为 NDIS。 如果 NDPROXY 定位与 TAPI 应用程序，NDPROXY 调用传递的字符串匹配的字符串与 SAP **NdisMCmCreateVc**设置具有 NDISWAN 它可以在其调度传入呼叫通知的连接终结点。 NDIS 反过来调用 NDISWAN 的*ProtocolCoCreateVc*函数并传递一个表示 VC 句柄。

-   NDPROXY 设置与 NDISWAN 的连接终结点后，它会调用[ **NdisCmDispatchIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdispatchincomingcall)函数，以通知 NDISWAN 有关传入调用。 在此调用，NDPROXY 传递封装的共同\_AF\_TAPI\_传入\_调用\_参数结构，其中包含传入的调用参数。 NDIS 反过来调用 NDISWAN 的*ProtocolClIncomingCall*函数，在其中 NDISWAN 接受或拒绝请求的连接。

-   决定是否接受连接后之后，可能更改调用参数，调用 NDISWAN **NdisClIncomingCallComplete**函数。 NDIS 反过来调用微型端口驱动程序*ProtocolCmIncomingCallComplete*函数。 具体取决于是否 NDISWAN 接受传入呼叫和微型端口驱动程序是否接受或拒绝 NDISWAN 的调用参数的更改提议，微型端口驱动程序拨打**NdisCmDispatchCallConnected**或**NdisCmDispatchIncomingCloseCall**函数。 **NdisCmDispatchCallConnected**通知 NDISWAN 微型端口驱动程序创建传入调用 VC 可以开始数据传输。 **NdisCmDispatchIncomingCloseCall**通知 NDISWAN 和 NDPROXY 关闭传入呼叫。

-   NDISWAN 接受传入的调用后，调用 NDPROXY [ **NdisCoGetTapiCallId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscogettapicallid)函数来检索一个字符串，标识为 VC NDISWAN 的上下文。 NDPROXY 将此字符串传递回 TAPI 应用程序。 TAPI 应用程序使用此 VC 上下文字符串来完成对其调用**lineGetID**。

 

 





