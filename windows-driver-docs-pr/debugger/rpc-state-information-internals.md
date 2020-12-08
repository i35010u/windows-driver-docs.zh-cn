---
title: RPC 状态信息的内部结构
description: RPC 状态信息的内部结构
keywords:
- RPC 调试，RPC 状态信息内部
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0268fe44cb1934c64a766f30b98cb457fd93c161
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786929"
---
# <a name="rpc-state-information-internals"></a>RPC 状态信息的内部结构


## <span id="ddk_rpc_state_information_internals_dbg"></span><span id="DDK_RPC_STATE_INFORMATION_INTERNALS_DBG"></span>


本部分提供 RPC 运行时收集的状态信息的内部结构的详细信息。

所有 RPC 运行时状态信息都包含在单元格中。 单元是可单独查看和更新的信息的最小单位。

RPC Run-Time 中的每个密钥对象将维护一个或多个有关其状态的信息单元。 每个单元都有一个单元 ID。 当对象引用另一对象时，它通过指定该对象的单元 ID 来实现此目的。 RPC Run-Time 可以维护的关键对象包括终结点、线程、连接对象、服务器调用 (SCALL) 对象和客户端调用 (CCALL) 对象。

**当 rpc 服务器正在运行时**，rpc Run-Time 使用一个或多个工作线程侦听一组终结点。 每次将数据传输到服务器时，线程会选取数据并确定传入请求的内容。 如果请求要创建连接，将创建一个连接对象，然后此对象将对该连接的所有调用进行服务。 对连接进行 RPC 调用时，连接对象会将服务器调用实例化 (与客户端调用) 对象 (CCALL) 对象。 然后，此服务器调用对象处理此特定调用。

**当 rpc 客户端正在运行时**，每次进行调用时，rpc Run-Time 都将创建一个客户端调用对象。 此客户端调用对象包含有关此特定调用的信息。

### <a name="span-idendpoint_cellsspanspan-idendpoint_cellsspanendpoint-cells"></a><span id="endpoint_cells"></span><span id="ENDPOINT_CELLS"></span>终结点单元

从 RPC 运行时的角度来看，终结点是可以与特定服务器联系的入口点。 终结点始终与给定的 RPC 传输相关联。 终结点状态信息用于将客户端调用与服务器上的特定进程相关联。

终结点单元格中的字段为：

<span id="ProtseqType"></span><span id="protseqtype"></span><span id="PROTSEQTYPE"></span>**ProtseqType**  
此终结点的协议顺序。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
状态值：已 *分配*、 *活动* 或 *非活动* 状态。 大多数终结点处于活动状态。 当创建进程已启动，但尚未完成时，终结点的状态为 "已 *分配* "。 如果某个终结点不再处于使用状态，则该终结点处于不 *活动状态* (例如，当已卸载某个协议) 。

<span id="EndpointName"></span><span id="endpointname"></span><span id="ENDPOINTNAME"></span>**点**  
终结点名称的前28个字符。

### <a name="span-idthread_cellsspanspan-idthread_cellsspanthread-cells"></a><span id="thread_cells"></span><span id="THREAD_CELLS"></span>线程单元

服务器线程是 (标准 Win32 线程的工作线程，供 RPC) 使用。

线程单元中的字段为：

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
状态值： *处理*、 *调度*、 *分配* 或 *空闲*。 *处理* 线程是 Run-Time 中的线程，正在处理信息。 已 *调度的线程已* 调度 (调用) 到服务器提供的管理器例程， (通常只是调用 *服务器例程*) 。 已缓存 *分配* 的线程。 *空闲* 线程可用于服务请求。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
上次更新信息后) 启动之后 (的时间（以毫秒为单位）。

<span id="TID"></span><span id="tid"></span>**TID**  
此线程的线程 ID。 尝试与调试器中的线程列表相关联时，这非常有用。

### <a name="span-idconnection_object_cellsspanspan-idconnection_object_cellsspanconnection-object-cells"></a><span id="connection_object_cells"></span><span id="CONNECTION_OBJECT_CELLS"></span>连接对象单元

连接对象单元中的字段为：

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
标志值包括 *独占* / 的 *非独占*、*身份验证级别* 和 *身份验证服务*。

<span id="LastTransmitFragmentSize"></span><span id="lasttransmitfragmentsize"></span><span id="LASTTRANSMITFRAGMENTSIZE"></span>**LastTransmitFragmentSize**  
通过连接传输的最后一个片段的大小。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**终结点**  
从中提取此连接的终结点的单元 ID。

<span id="LastSendTime"></span><span id="lastsendtime"></span><span id="LASTSENDTIME"></span>**LastSendTime**  
上次在连接上发送数据的时间。

<span id="LastReceiveTime"></span><span id="lastreceivetime"></span><span id="LASTRECEIVETIME"></span>**LastReceiveTime**  
上次连接时接收数据的时间。

### <a name="span-idserver_call_object_cellsspanspan-idserver_call_object_cellsspanserver-call-object-cells"></a><span id="server_call_object_cells"></span><span id="SERVER_CALL_OBJECT_CELLS"></span>服务器调用对象单元

服务器调用中 (SCALL) 对象单元的字段如下：

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
状态值：已 *分配*、 *活动* 或已 *分派*。 *分配* 的调用处于非活动状态并且已缓存。 当调用处于 *活动状态* 时，RPC Run-Time 正在处理与此调用有关的信息。 *分派* 调用时， (server 例程) 的管理器例程已被调用，但尚未返回。

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
此调用的 "netmon 捕获文件") 中 (操作编号的过程号。 RPC Run-Time 从接口标识各个例程，方法是在 IDL 文件中按位置对它们进行编号。 接口中的第一个例程将为数字零，第二个值为1，依此类推。

<span id="InterfaceUUIDStart"></span><span id="interfaceuuidstart"></span><span id="INTERFACEUUIDSTART"></span>**InterfaceUUIDStart**  
接口 UUID 的第一个 DWORD。

<span id="ServicingTID"></span><span id="servicingtid"></span><span id="SERVICINGTID"></span>**ServicingTID**  
正在为此调用提供服务的线程的单元 ID。 如果调用不 *处于活动状态* 或已 *调度*，则包含过期信息。

<span id="CallFlags"></span><span id="callflags"></span><span id="CALLFLAGS"></span>**CallFlags**  
这些标志值指示这是否是一个独占连接中的缓存调用，无论这是否是一个异步调用，这是否是一个管道调用，以及这是否是 LRPC 或 OSF 调用。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
上次更新调用对象状态信息后) 启动之后 (的时间（以毫秒为单位）。

<span id="PID"></span><span id="pid"></span>**P&ID**  
调用方的进程 ID。 仅对 LRPC 调用有效。

<span id="TID"></span><span id="tid"></span>**TID**  
调用方的线程 ID。 仅对 LRPC 调用有效。

### <a name="span-idclient_call_object_cellsspanspan-idclient_call_object_cellsspanclient-call-object-cells"></a><span id="client_call_object_cells"></span><span id="CLIENT_CALL_OBJECT_CELLS"></span>客户端调用对象单元

 (CCALL) 对象的客户端调用被分解为两个单元，因为有关客户端调用的信息太大，无法容纳在一个单元中。 第一个单元格称为 *客户端调用信息*，第二个单元称为 *调用目标信息*。 大多数工具会将信息一起显示，因此您无需区分它们。

除非正在收集完整的状态信息，否则不会维护有关客户端调用的信息。 此规则有一个例外：即使在收集服务器状态信息时，也会保留有关在服务器调用中进行的客户端调用的信息。 这允许跟踪跨多个跃点的调用。

客户端调用信息单元中的字段为：

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
步骤编号 (操作编号，netmon 用于捕获正在调用的方法) 的文件。 RPC Run-Time 从接口标识各个例程，方法是在 IDL 文件中按位置对它们进行编号。 接口中的第一个例程将为数字零，第二个值为1，依此类推。

<span id="ServicingThread"></span><span id="servicingthread"></span><span id="SERVICINGTHREAD"></span>**ServicingThread**  
进行此调用的线程的单元 ID。

<span id="IfStart"></span><span id="ifstart"></span><span id="IFSTART"></span>**IfStart**  
进行调用的接口 UUID 的第一个 DWORD。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**终结点**  
进行调用的服务器上的终结点的前12个字符。

调用目标信息单元中的字段为：

<span id="ProtocolSequence"></span><span id="protocolsequence"></span><span id="PROTOCOLSEQUENCE"></span>**ProtocolSequence**  
此调用的协议序列。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
当客户端调用信息或调用目标的信息更新时，启动) 后 (以毫秒为单位。

<span id="TargetServer"></span><span id="targetserver"></span><span id="TARGETSERVER"></span>**TargetServer**  
调用的服务器的名称的前24个字符。

 

 





