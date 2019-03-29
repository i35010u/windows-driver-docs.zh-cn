---
title: RPC 状态信息的内部结构
description: RPC 状态信息的内部结构
ms.assetid: fac4a1e4-e1ec-41f2-8de9-073a04a979be
keywords:
- RPC 调试 RPC 状态信息内部机制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6445fd83745dfaa98e2b52ab5f3692da18fbe87d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565333"
---
# <a name="rpc-state-information-internals"></a>RPC 状态信息的内部结构


## <span id="ddk_rpc_state_information_internals_dbg"></span><span id="DDK_RPC_STATE_INFORMATION_INTERNALS_DBG"></span>


本部分提供了收集通过 RPC 运行时的状态信息的内部结构的详细信息。

RPC 运行时状态的所有信息都包含在单元格。 单元格是信息的可以查看和更新单独的最小单位。

每个键的对象中 RPC 运行时将保持其状态信息的一个或多个单元格。 每个单元格有一个单元格的 id。 当对象引用另一个对象时，它是通过指定该对象的单元格 id。 RPC 运行时可以维护有关的信息的关键对象是终结点、 线程、 连接对象、 服务器调用 (SCALL) 对象和客户端调用 (CCALL) 对象。

**RPC 服务器运行时**，RPC 运行时在一组终结点使用一个或多个工作线程上进行侦听。 每当数据传输到服务器，一个线程提取数据，并确定传入请求。 如果请求是要创建的连接，创建一个连接对象，和此对象然后服务在连接上的所有调用。 在连接上建立的 RPC 调用后，连接对象实例化一个对应于客户端调用 (CCALL) 对象的服务器调用 (SCALL) 对象。 此服务器调用对象随后处理此特定调用。

**RPC 客户端运行时**，RPC 运行时进行调用，每次创建客户端调用的对象。 此客户端调用的对象包含有关此特定调用的信息。

### <a name="span-idendpointcellsspanspan-idendpointcellsspanendpoint-cells"></a><span id="endpoint_cells"></span><span id="ENDPOINT_CELLS"></span>终结点的单元格

RPC 运行时的角度来看，从终结点是可以通过它联系特定的服务器的入口点。 终结点是始终与给定的 RPC 传输相关联。 终结点状态信息用于将客户端的调用与服务器上的特定进程相关联。

在终结点单元格中的字段是：

<span id="ProtseqType"></span><span id="protseqtype"></span><span id="PROTSEQTYPE"></span>**ProtseqType**  
此终结点协议序列。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
状态值：*分配*， *active*，或*处于非活动状态*。 大多数终结点处于活动状态。 终结点有*分配*时创建过程已启动，但还没有完成的状态。 终结点是*处于非活动状态*如果它不再使用 （例如，如果已卸载协议）。

<span id="EndpointName"></span><span id="endpointname"></span><span id="ENDPOINTNAME"></span>**EndpointName**  
终结点名称的前 28 个字符。

### <a name="span-idthreadcellsspanspan-idthreadcellsspanthread-cells"></a><span id="thread_cells"></span><span id="THREAD_CELLS"></span>线程的单元格

服务器线程是工作线程 （即标准 Win32 线程，以供 RPC）。

线程单元中的字段是：

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
状态值：*处理*，*调度*，*分配*，或者*空闲*。 一个*处理*线程是指在运行时内并且正在处理的信息。 一个*调度*具有已调度线程 （称为） 提供服务器管理器例程 (通常简称为*server 例程*)。 *分配*线程进行了缓存。 *空闲*线程可供服务请求。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
上次更新的信息 （以毫秒为单位，启动后） 时间。

<span id="TID"></span><span id="tid"></span>**TID**  
此线程的线程 ID。 尝试将与在调试器中主题列表相关联时，这很有用。

### <a name="span-idconnectionobjectcellsspanspan-idconnectionobjectcellsspanconnection-object-cells"></a><span id="connection_object_cells"></span><span id="CONNECTION_OBJECT_CELLS"></span>连接对象的单元格

连接对象单元中的字段是：

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**标志**  
标志的值包括*独占*/*非排他*，*身份验证级别*，并且*身份验证服务*。

<span id="LastTransmitFragmentSize"></span><span id="lasttransmitfragmentsize"></span><span id="LASTTRANSMITFRAGMENTSIZE"></span>**LastTransmitFragmentSize**  
通过连接传输的最后一个片段的大小。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**终结点**  
单元格从选取此连接的终结点的 ID。

<span id="LastSendTime"></span><span id="lastsendtime"></span><span id="LASTSENDTIME"></span>**LastSendTime**  
在连接上发送的最后一个时间数据。

<span id="LastReceiveTime"></span><span id="lastreceivetime"></span><span id="LASTRECEIVETIME"></span>**LastReceiveTime**  
在连接上收到的最后一个时间数据。

### <a name="span-idservercallobjectcellsspanspan-idservercallobjectcellsspanserver-call-object-cells"></a><span id="server_call_object_cells"></span><span id="SERVER_CALL_OBJECT_CELLS"></span>服务器调用对象的单元格

服务器调用 (SCALL) 对象单元中的字段是：

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
状态值：*分配*， *active*，或*调度*。 *分配*调用已停用，缓存。 调用何时*active*，RPC 运行时正在处理与此调用相关的信息。 调用何时*调度*，管理器例程 （server 例程） 已调用，并且未尚未返回。

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
此调用过程号 （netmon 捕获文件中，操作数量）。 RPC 运行时按编号的 IDL 文件中的位置标识接口中的单个例程。 在界面中的第一个例程将数字零，第二个第一位，依次类推。

<span id="InterfaceUUIDStart"></span><span id="interfaceuuidstart"></span><span id="INTERFACEUUIDSTART"></span>**InterfaceUUIDStart**  
接口 UUID 的第一个 dword 值。

<span id="ServicingTID"></span><span id="servicingtid"></span><span id="SERVICINGTID"></span>**ServicingTID**  
单元格所服务的此调用的线程 ID。 如果不是在调用*active*或*调度*，这包含过时的信息。

<span id="CallFlags"></span><span id="callflags"></span><span id="CALLFLAGS"></span>**CallFlags**  
这些标志值指示这是否这是否是一个管道调用，这是异步调用，以及是否这是一个 LRPC 或 OSF 调用是独占的连接中的缓存的调用。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
上次更新的时间 （以毫秒为单位，启动后） 时调用对象的状态信息。

<span id="PID"></span><span id="pid"></span>**PID**  
调用方的进程 ID。 仅对 LRPC 调用有效。

<span id="TID"></span><span id="tid"></span>**TID**  
调用方线程 ID。 仅对 LRPC 调用有效。

### <a name="span-idclientcallobjectcellsspanspan-idclientcallobjectcellsspanclient-call-object-cells"></a><span id="client_call_object_cells"></span><span id="CLIENT_CALL_OBJECT_CELLS"></span>客户端调用对象的单元格

客户端调用 (CCALL) 对象分为两个单元格，因为太大，无法容纳在一个单元格中有关客户端调用的信息。 调用第一个单元格*客户端调用信息*，而第二个称为*调用目标信息*。 大多数工具将在一起，显示的信息，因此不需要区分它们。

除非您要收集完整的状态信息不会保留有关客户端调用的信息。 此规则的例外： 即使仅服务器状态信息在收集维护有关进行中的服务器调用的客户端调用的信息。 这样可以跨越多个跃点跟踪的调用。

客户端调用信息单元中的字段是：

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
要调用的方法过程号 （netmon 捕获文件中，操作数量）。 RPC 运行时按编号的 IDL 文件中的位置标识接口中的单个例程。 在界面中的第一个例程将数字零，第二个第一位，依次类推。

<span id="ServicingThread"></span><span id="servicingthread"></span><span id="SERVICINGTHREAD"></span>**ServicingThread**  
其进行此调用线程的单元格 ID。

<span id="IfStart"></span><span id="ifstart"></span><span id="IFSTART"></span>**IfStart**  
在其调用接口 UUID 的第一个 dword 值。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**终结点**  
对其进行调用的服务器上的终结点前 12 个字符。

调用目标信息单元中的字段是：

<span id="ProtocolSequence"></span><span id="protocolsequence"></span><span id="PROTOCOLSEQUENCE"></span>**ProtocolSequence**  
此调用协议序列。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
有关客户端调用或调用目标的信息已更新时 （以毫秒为单位，启动后） 的时间。

<span id="TargetServer"></span><span id="targetserver"></span><span id="TARGETSERVER"></span>**TargetServer**  
对其进行调用的服务器的名称前 24 个字符。

 

 





