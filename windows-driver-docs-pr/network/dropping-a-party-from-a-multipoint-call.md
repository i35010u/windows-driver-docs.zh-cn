---
title: 从 Multipoint 调用删除参与方
description: 从 Multipoint 调用删除参与方
ms.assetid: db23e911-7c70-432e-992a-fdfdf8cb28ae
keywords:
- WDK 的 CoNDIS 的参与方
- 多点调用 WDK 的 CoNDIS
- 从 multipoint 调用删除参与方
- 从 multipoint 调用中删除参与方
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a5c3775dad289a577d688db78ee22f2de438d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522936"
---
# <a name="dropping-a-party-from-a-multipoint-call"></a>从 Multipoint 调用删除参与方





可用作多点调用的根最终必须从与该调用中删除每个参与方的面向连接的客户端[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)或[ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627).

客户端将在以下情况下调用删除参与方：

-   使用多点调用的向下启动拆解前**NdisClCloseCall**(请参阅[Client-Initiated 请求关闭调用](client-initiated-request-to-close-a-call.md))，客户端必须删除与对连续调用的最后一个参与方以外的所有**NdisClDropParty**。 客户端指定要从与调用中删除的最后一个参与方**NdisClCloseCall**。

-   响应远程方的请求删除从 multipoint 调用 (请参阅[传入请求，从 Multipoint 调用中删除参与方](incoming-request-to-drop-a-party-from-a-multipoint-call.md))，客户端，从其[ **ProtocolClIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff570231)函数，将调用**NdisClDropParty**。

客户端的调用**NdisClDropParty** NDIS 调用将导致[ **ProtocolCmDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff570244)呼叫管理器或共享相同的 MCM 驱动程序的函数*NdisVcHandle*到 multipoint VC。

下图显示调用的客户端管理器请求从 multipoint 调用删除参与方。

![说明调用管理器请求从 multipoint 调用删除参与方的客户端的关系图](images/cm-18.png)

下图显示了客户端的请求从 multipoint 调用删除参与方的 MCM 驱动程序。

![说明客户端的请求从 multipoint 调用删除参与方的 mcm 驱动程序的关系图](images/fig1-18.png)

*ProtocolCmDropParty*与网络控制设备，若要从现有的多点调用删除参与方进行通信。 NDIS 可以传递给*ProtocolCmDropParty*指向包含数据的缓冲区的指针 (提供给客户端在调用**NdisClDropParty**)。 *ProtocolCmDropParty*必须任何此类数据在网络上发送之前删除该连接。

*ProtocolCmDropParty*可以使用完成同步，或更可能，以异步方式[ **NdisCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561674)，在调用管理器的情况下或[ **NdisMCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563543)，在 MCM 驱动程序的情况下。

在调用**Ndis (M) CmDropPartyComplete**会导致调用客户端的 NDIS [ **ProtocolClDropPartyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570227)函数。 如果客户端的过程中创建的它关闭 multipoint VC *ProtocolClDropPartyComplete*可以调用**NdisClDropParty**与任何有效*NdisPartyHandle*到一个在客户端的 active multipoint VC 其余的参与方。 如果只有一个参与方保留在其 multipoint VC 上，客户端应表示通过删除该参与方及其*NdisPartyHandle*到**NdisClCloseCall**(请参阅[Client-Initiated 请求关闭调用](client-initiated-request-to-close-a-call.md)).

 

 





