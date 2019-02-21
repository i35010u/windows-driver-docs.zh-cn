---
title: 在 NDIS 6.80 同步 OID 请求接口
description: 本主题介绍在 NDIS 6.80 中的新同步 OID 请求接口
ms.assetid: 6BF2E800-90A0-48FC-B702-5AD4EC318A35
keywords: 同步 OID 请求接口，同步 OID 调用，WDK 同步 Oid 同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 834028856064246b1c74282574cadda65b1b4788
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533587"
---
# <a name="synchronous-oid-request-interface-in-ndis-680"></a>在 NDIS 6.80 同步 OID 请求接口

Windows 网络驱动程序使用 OID 请求发送控制 NDIS 绑定在堆栈的下层的消息。 协议驱动程序，如 TCPIP 或 vSwitch，依赖于多个 Oid 配置基础 NIC 驱动程序的每个功能。 在 Windows 10 版本 1709 前, 两种方式发送 OID 请求：常规和直接。 

本主题介绍 OID 调用的第三个样式：同步。 同步调用用于进行低延迟、 非阻止性、 伸缩性和可靠性。 可在 NDIS 6.80，包含在 Windows 10 版本 1709年及更高版本中启动同步 OID 请求接口。

## <a name="comparison-to-regular-and-direct-oid-requests"></a>与常规模式和直接 OID 请求之间的比较

与同步 OID 请求负载调用 (OID 本身) 完全是与常规模式和直接 OID 请求相同。 对于调用本身是唯一的区别。 因此，*什么*是相同的所有三种类型的 Oid; 仅*如何*不同。

下表描述了正则 Oid、 直接 Oid 和同步 Oid 之间的差异。

| | 正则 OID | 直接 OID | 同步的 OID |
| --- | --- | --- | --- |
| 有效负载 | [NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710) | NDIS_OID_REQUEST | NDIS_OID_REQUEST |
| OID 类型 | 统计信息的查询中，集方法 | 统计信息的查询中，集方法 | 统计信息的查询中，集方法 |
| 可以通过发出 | 协议，筛选器 | 协议，筛选器 | 协议，筛选器 |
| 可以通过完成 | 微型端口筛选器 | 微型端口筛选器 | 微型端口筛选器 |
| 可以修改筛选器 | 是 | 是 | 是 |
| NDIS 分配内存 | 对于每个筛选器 （OID 克隆） | 对于每个筛选器 （OID 克隆） | 仅当极大量的筛选器 （调用上下文） |
| 可以挂起 | 是 | 是 | 否 |
| 可以阻止 | 是 | 否 | 否 |
| IRQL | = = 被动 | \<= DISPATCH | \<= DISPATCH |
| [序列化的 NDIS](miniport-adapter-oid-request-serialization.md) | 是 | 否 | 否 |
| 调用筛选器 | 以递归方式 | 以递归方式 | 以迭代方式 |
| 筛选器克隆 OID | 是 | 是 | 否 |

## <a name="filtering"></a>筛选

其他两种类型的 OID 的调用，如筛选器驱动程序中同步调用可以完全控制 OID 请求。 筛选器驱动程序可以观察到，截获、 修改和颁发同步 Oid。 但是，为了提高效率，同步 OID 的机制是略有不同。

### <a name="passthrough-interception-and-origination"></a>传递、 拦截和来源

从概念上讲，所有 OID 请求从更高版本的驱动程序发出和完成的较低的驱动程序。 此过程中，OID 请求可能会通过任意数量的筛选器驱动程序。

在最常见的情况下，协议驱动程序将发出一个 OID 请求和所有筛选器只需传递下，未修改的 OID 请求。 下图说明了这种常见方案。

![典型的 OID 路径源自协议](images/synchronous_oids_oid_path_full.png "典型 OID 路径源自一个协议")

但是，允许任何筛选器模块截取 OID 请求，并完成它。 在这种情况下，请求不会通过较低的驱动程序，如以下关系图中所示。

![典型的 OID 路径源自协议和筛选器被截获](images/synchronous_oids_oid_path_intercepted.png "典型 OID 路径源自协议和截获筛选器")

在某些情况下，筛选器模块可能决定源于自己 OID 的请求。 此请求从筛选器模块的级别开始，并仅遍历低级驱动程序，如下图所示。

![从筛选器的典型 OID 路径发起](images/synchronous_oids_oid_path_filter_originated.png "典型 OID 路径源自一个筛选器")

OID 的所有请求都具有此基本流： 更高版本的驱动程序 （一个协议或筛选器驱动程序） 发出的请求和较低的驱动程序 （一个微型端口或筛选器驱动程序） 完成后，它。

### <a name="how-regular-and-direct-oid-requests-work"></a>如何定期和 Direct OID 的请求的工作

常规连接或直接 OID 请求是调度以递归方式。 下图显示了函数调用序列。 请注意，序列本身非常类似于在上一节中，从关系图中描述的顺序排列显示请求的递归性质。

![函数调用序列的常规模式和直接 OID 请求](images/synchronous_oids_regular_oid_request_sequence.png "常规模式和直接 OID 请求的函数调用序列")

如果没有安装足够筛选器，则会强制 NDIS 以分配新的线程堆栈，以使递归更深入。

NDIS 会考虑[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构保持有效的仅单跃点沿堆栈。 如果筛选器驱动程序想要传递到下一个较低驱动程序 （这是大多数 Oid 的这种情况），请求筛选器驱动程序*必须*插入的样板文件代码以克隆 OID 请求多个几十个行。 这一样板具有几个问题：

1. 它强制要克隆 OID 的内存分配。 达到内存池既缓慢又会导致无法保证 OID 请求的向前推进。
2. OID 结构设计必须保持不变随着时间的推移因为 all 的筛选器驱动程序硬编码的一个 NDIS_OID_REQUEST 的内容复制到另一种机制。
3. 需要如此多样板会遮盖筛选器的真正作用。

### <a name="the-filtering-model-for-synchronous-oid-requests"></a>用于同步的 OID 请求筛选的模型

同步 OID 请求筛选模型利用的同步调用，以解决在上一节中讨论的问题性质。

#### <a name="issue-and-complete-handlers"></a>问题和已完成处理程序

与常规模式和直接 OID 请求不同有两个筛选器挂钩，对于同步 OID 请求： 一个问题处理程序和完成处理程序。 既不、 一个或两个挂钩，可以注册筛选器驱动程序。

问题的调用会调用每个筛选器驱动程序，从堆栈的底部到堆栈的顶部开始。 任何筛选器的问题调用可停止继续向下拖动，OID 并完成，状态代码为某些 OID。 如果任何筛选器不决定截获 OID，OID 达到 NIC 驱动程序，它必须以同步方式完成 OID。

OID 完成后，完整的调用会调用每个筛选器驱动程序，从任何位置堆栈中 OID 完成时，最多堆栈的顶部开始。 完整的调用可以检查或修改 OID 请求，并检查或修改 OID 的完成状态代码。

下图说明了典型的示例中，其中一种协议发出的同步 OID 请求和筛选器不截获请求。

![函数调用序列同步 OID 请求](images/synchronous_oids_synchronous_oid_request_sequence.png "同步 OID 请求的函数调用序列")

请注意同步 Oid 的调用模型是迭代。 这会使受常量，无需不断展开堆栈的堆栈使用。

如果筛选器驱动程序截获其问题的处理程序中同步 OID，OID 不是提供给较低的筛选器或 NIC 驱动程序。 但是，仍调用完成处理程序的更高版本的筛选器，如以下关系图中所示：

![按筛选器函数调用序列的同步 OID 请求的拦截](images/synchronous_oids_synchronous_oid_request_sequence_intercepted.png "的同步 OID 请求的筛选器拦截函数调用序列")

#### <a name="minimal-memory-allocations"></a>最小内存分配

常规模式和直接 OID 请求需要克隆 NDIS_OID_REQUEST 使用筛选器驱动程序。 与此相反，不允许同步 OID 请求要克隆。 此设计的优势是同步的 Oid 具有较低的延迟 – OID 请求不重复克隆下筛选器堆栈中 – 传输时，有故障的可能性更小。

但是，它会引发新问题。 如果不能克隆 OID，其中筛选器驱动程序中 does 存储其每个请求状态呢？ 例如，假设筛选器驱动程序将转换到另一个 OID。 在堆栈的方式，需要关闭旧 OID 保存筛选器。 在备份堆栈的方式，筛选器需要还原旧的 OID。

若要解决此问题，NDIS 对于每个筛选器驱动程序，为每个正在进行的同步 OID 请求分配的指针大小的槽。 NDIS 会在其完成处理程序从筛选器的问题处理程序调用保留此槽。 这样，要关闭更高版本使用的完成处理程序的状态将保存的问题处理程序。 以下代码段演示了示例。

```cpp
NDIS_STATUS
MyFilterSynchronousOidRequest(
  _In_ NDIS_HANDLE FilterModuleContext,
  _Inout_ NDIS_OID_REQUEST *OidRequest,
  _Outptr_result_maybenull_ PVOID *CallContext)
{
  if ( . . . should intercept this OID . . . )
  {
    // preserve the original buffer in the CallContext
    *CallContext = OidRequest->DATA.SET_INFORMATION.InformationBuffer;

    // replace the buffer with a new one
    OidRequest->DATA.SET_INFORMATION.InformationBuffer = . . . something . . .;
  }

  return NDIS_STATUS_SUCCESS;
}

VOID
MyFilterSynchronousOidRequestComplete(
  _In_ NDIS_HANDLE FilterModuleContext,
  _Inout_ NDIS_OID_REQUEST *OidRequest,
  _Inout_ NDIS_STATUS *Status,
  _In_ PVOID CallContext)
{
  // if the context is not null, we must have replaced the buffer.
  if (CallContext != null)
  {
    // Copy the data from the miniport back into the protocol’s original buffer.
    RtlCopyMemory(CallContext, OidRequest->DATA.SET_INFORMATION.InformationBuffer,...);
     
    // restore the original buffer into the OID request
    OidRequest->DATA.SET_INFORMATION.InformationBuffer = CallContext;
  }
}
```

NDIS 将保存每个筛选器每次调用一个 PVOID。 NDIS 会试探性地分配合理的堆栈上的槽数，以便有零个池分配的常见情况下。 这通常是不超过七个筛选器。 如果用户设置了一种反常情况，NDIS does 故障回复到的池分配。

#### <a name="reduced-boilerplate"></a>减少的样本

在考虑样板[用于处理常规连接或直接 OID 请求示例样板](example-boilerplate-for-handling-regular-or-direct-oid-requests.md)。 该代码是只是要注册的 OID 处理程序条目的成本。 如果你想要发出您自己的 Oid，您必须添加另一个编写几十行样本。 与同步 Oid，不是需要处理异步完成的其他复杂问题。 因此，您可以剪切掉许多样板。

下面是使用同步 Oid 的最小问题处理程序：

```cpp
NDIS_STATUS
MyFilterSynchronousOidRequest(
  NDIS_HANDLE FilterModuleContext,
  NDIS_OID_REQUEST *OidRequest,
  PVOID *CallContext)
{
  return NDIS_STATUS_SUCCESS;
}
```

如果你想要截获或更改特定 OID，可以通过添加几行代码来执行它。 最小的完成处理程序是更简单：

```cpp
VOID
MyFilterSynchronousOidRequestComplete(
  NDIS_HANDLE FilterModuleContext,
  NDIS_OID_REQUEST *OidRequest,
  NDIS_STATUS *Status,
  PVOID CallContext)
{
  return;
}
```

同样，筛选器驱动程序可以发出新的同步 OID 请求的自己的仅使用一行代码：

```cpp
status = NdisFSynchronousOidRequest(binding->NdisBindingHandle, &oid);
```

与此相反，必须颁发常规或直接 OID 的筛选器驱动程序必须设置异步完成处理程序，并实现一些代码来区分其自己的只是克隆的 Oid 完成中的 OID 完成。 上的这一样板示例[发出的正则 OID 请求示例样板](example-boilerplate-for-issuing-a-regular-oid-request.md)。

## <a name="interoperability"></a>互操作性

尽管常规、 直接和同步调用样式所有使用相同的数据结构，管道不会给微型端口在同一处理程序。 此外，不能在一些管道中使用某些 Oid。 例如， [OID_PNP_SET_POWER](oid-pnp-set-power.md)需要小心同步，并且通常会强制要求微型端口，以便进行阻止调用。 这使处理它很难在直接 OID 回调并防止在同步 OID 回调中的使用它。 

因此，正如同直接 OID 请求同步 OID 调用仅可使用 Oid 的子集。 在 Windows 10 版本 1709，仅[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)中使用 OID[接收端缩放版本 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)支持同步 OID 路径中。

## <a name="implementing-synchronous-oid-requests"></a>实现同步 OID 请求

在驱动程序中实现同步 OID 请求接口的详细信息，请参阅以下主题：

- [微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)
- [筛选模块 OID 请求](filter-module-oid-requests.md)
- [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)

