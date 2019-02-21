---
title: 使传出调用
description: 使传出调用
ms.assetid: 295b3f6d-d53b-4030-b7e9-35ab7524d9aa
keywords:
- CoNDIS WAN 的驱动程序 WDK 网络拨出电话
- WDK WAN，拨出电话的电话服务
- 拨出电话的 CoNDIS TAPI WDK 网络
- WDK 的 CoNDIS WAN 的传出呼叫
- 调用 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23022830173e92f28af2c28192824bc68dcfdc02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521826"
---
# <a name="making-outgoing-calls"></a>使传出调用





如果应用程序尝试发起传出呼叫，它必须首先打开一个行。 由于调用 TAPI 的应用程序打开一个行**lineOpen**函数。 若要在以前打开的行上发出电话呼叫，应用程序调用 TAPI **lineMakeCall**函数，并将指针传递到特定的目标地址。 如果除默认调用安装程序将请求参数，该应用程序还将指针传递给 LINECALLPARAMS 结构。 如果应用程序使用默认调用安装程序参数**lineMakeCall**提供 LINECALLPARAMS 结构中的这些参数。 此结构的成员指定电话服务调用应如何设置。

这些 TAPI 函数调用会导致 NDPROXY 驱动程序首先通过 WAN 的 CoNDIS 微型端口驱动程序创建的虚拟连接 (VC)，然后封装 TAPI NDIS 中的参数结构才能发起传出呼叫。 微型端口驱动程序将使用这些 TAPI 参数来设置传出呼叫。 下面介绍连接、 设置和进行传出呼叫的方式：

-   NDPROXY 调用[ **NdisCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561696)若要启动的微型端口驱动程序与 VC 创建。 NDPROXY 后，将调用**NdisCoCreateVc**，NDIS 调用，以与同步操作*ProtocolCoCreateVc*呼叫管理器的功能集成到微型端口驱动程序。 NDIS 将传递给*ProtocolCoCreateVc*表示 VC 的句柄。 如果在调用**NdisCoCreateVc**是成功，NDIS 填充并返回 VC 句柄。 *ProtocolCoCreateVc*执行任何必要的分配的动态资源和微型端口调用管理器 (MCM) 驱动程序需要执行后续操作更高版本将激活 VC 的结构。 此类资源包括但不限于内存缓冲区、 数据结构、 事件和其他此类类似资源。

-   NDPROXY 指定在传出呼叫的 TAPI 参数[**共同\_AF\_TAPI\_使\_调用\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545373)结构。 NDPROXY 填充此结构的成员使用以下信息在 TAPI 中传递**lineMakeCall**函数：
    -   中的目标地址**DestAddress**成员
    -   中的打开行标识符**ulLineID**成员
    -   在结构 LINECALLPARAMS **LineCallParams**成员
-   NDPROXY 叠加产生的 CO\_AF\_TAPI\_使\_调用\_参数结构上**参数**隶属[**共同\_特定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545396)结构和集**长度**成员产生的 CO\_特定\_产生的 CO 大小参数\_AF\_TAPI\_使\_调用\_参数。

-   NDPROXY 设置产生的 CO\_特定\_参数结构**MediaSpecific**的成员[**共同\_媒体\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545388)结构。

-   NDPROXY 将指针设置为产生的 CO\_媒体\_参数结构**MediaParameters**的成员[**共同\_调用\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545384)结构。

-   一旦 NDPROXY 封装 TAPI 参数，调用 NDPROXY [ **NdisClMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561635)函数来发起传出呼叫。 在此函数调用中，NDPROXY 将指针传递到已填充共同\_调用\_参数结构。 反过来调用 NDIS [ **ProtocolCmMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570246) CoNDIS WAN 微型端口驱动程序的呼叫管理器的功能。 微型端口驱动程序应检查仅产生的 CO\_AF\_TAPI\_使\_调用\_参数结构嵌入在 CO\_调用\_参数。 在这种情况下，没有其他调用参数是有意义。 如果微型端口驱动程序随后会激活传出调用 VC，微型端口驱动程序会调用[ **NdisMCmActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562792)函数，并将指针传递到已填充共同\_调用\_参数。

-   后微型端口驱动程序具有与协商要为 VC 建立电话服务调用参数并为这些设置 NIC 的网络调用的参数，微型端口驱动程序调用[ **NdisMCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563544)函数来指示它已准备好进行数据将传输上 VC。 在此调用中，微型端口驱动程序必须将该句柄传递到 VC 和做电话服务调用参数的修改。

-   微型端口驱动程序必须修改**CallMgrParameters**成员产生的 CO\_调用\_参数结构，以指定的服务质量 (QoS 传输数据包，带宽等)。 若要设置此**CallMgrParameters**成员，微型端口驱动程序填充的成员[**共同\_调用\_MANAGER\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545381)结构和点到此结构**CallMgrParameters**。 例如，若要确定传输并以字节为单位的 VC 每秒接收的速度，微型端口驱动程序必须设置**PeakBandwidth**的成员**传输**和**接收**成员产生的 CO\_调用\_MANAGER\_参数。 **传输**并**接收**成员是流程规格结构。 有关流程规格结构的详细信息，请参阅 Microsoft Windows SDK。

-   如果微型端口驱动程序已修改电话服务调用的参数，则必须设置**标志**成员中产生的 CO\_调用\_调用的参数结构\_参数\_已更改。 为**NdisMCmMakeCallComplete**调用由微型端口驱动程序，NDIS 调用 NDPROXY *ProtocolClMakeCallComplete*函数来完成启动异步操作与**NdisClMakeCall**。

-   微型端口驱动程序已成功完成的传出调用后，NDPROXY 通知 TAPI 应用程序连接呼叫。 然后此 TAPI 应用程序调用 TAPI **lineGetID**函数来通知 NDPROXY 来查找相应的 CoNDIS 客户端。 在此**lineGetID**调用，TAPI 应用程序提供特定的 TAPI 设备类向其应用程序需要一个句柄的字符串。 NDPROXY 使用此字符串来找到以前注册的特定 TAPI 设备类的 SAP 的 CoNDIS 客户端。 如果 NDISWAN CoNDIS 客户端，则该字符串为 NDIS。 如果 NDPROXY 定位与 TAPI 应用程序，NDPROXY 调用传递的字符串匹配的字符串与 SAP [ **NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812)设置具有 NDISWAN 可以调度的连接终结点已发出的传出调用的通知。 NDIS 反过来调用 NDISWAN 的*ProtocolCoCreateVc*函数并传递一个表示 VC 句柄。

-   NDPROXY 设置与 NDISWAN 的连接终结点后，它会调用[ **NdisCmDispatchIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561664)函数，以通知 NDISWAN 有关传出呼叫。 在此调用，NDPROXY 传递封装的共同\_AF\_TAPI\_使\_调用\_参数结构，其中包含的传出调用的参数。 NDIS 反过来调用 NDISWAN 的*ProtocolClIncomingCall*函数，在其中 NDISWAN 接受或拒绝请求的连接。 如果 NDISWAN 更改传递给它的调用参数，它必须设置**标志**成员中产生的 CO\_调用\_调用的参数结构\_参数\_已更改。

-   决定是否接受连接后之后，可能更改调用参数，调用 NDISWAN [ **NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632)函数。 NDIS 反过来调用微型端口驱动程序*ProtocolCmIncomingCallComplete*函数。 具体取决于是否 NDISWAN 接受传出调用和微型端口驱动程序是否接受或拒绝 NDISWAN 的调用参数的更改提议，微型端口驱动程序拨打[ **NdisCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff561661)或[ **NdisCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561670)函数。 **NdisCmDispatchCallConnected**通知 NDISWAN 数据传输可以开始在为传出调用创建 NDPROXY VC。 **NdisCmDispatchIncomingCloseCall**通知 NDISWAN 和 NDPROXY 关闭建议传出呼叫。

-   NDISWAN 接受传出调用后，调用 NDPROXY [ **NdisCoGetTapiCallId** ](https://msdn.microsoft.com/library/windows/hardware/ff561700)函数来检索一个字符串，标识为 VC NDISWAN 的上下文。 NDPROXY 将此字符串传递回 TAPI 应用程序。 TAPI 应用程序使用此 VC 上下文字符串来完成对其调用**lineGetID**。

 

 





