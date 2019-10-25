---
title: NDIS 6.80 中的同步 OID 请求接口
description: 本主题介绍了 NDIS 6.80 中的新同步 OID 请求接口
ms.assetid: 6BF2E800-90A0-48FC-B702-5AD4EC318A35
keywords: 同步 OID 请求接口，同步 OID 调用，WDK 同步 Oid，同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1787e8ba74dba5f2e69674cd9272c33e601670d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841782"
---
# <a name="synchronous-oid-request-interface-in-ndis-680"></a>NDIS 6.80 中的同步 OID 请求接口

Windows 网络驱动程序使用 OID 请求，在 NDIS 绑定堆栈中发送控制消息。 协议驱动程序（如 TCPIP 或 vSwitch）依赖于几十个 Oid 来配置基础 NIC 驱动程序的每个功能。 在 Windows 10 版本1709之前，通过两种方式发送 OID 请求：常规和直接。 

本主题介绍了第三种类型的 OID 调用：同步。 同步调用应该是低延迟、非阻止、可缩放和可靠的。 从 Windows 10 版本1709及更高版本中包含的 NDIS 6.80 开始，同步 OID 请求接口可用。

## <a name="comparison-to-regular-and-direct-oid-requests"></a>与常规和直接 OID 请求的比较

对于同步 OID 请求，调用的有效负载（OID 本身）与常规和直接 OID 请求完全相同。 唯一的区别在于调用本身。 因此，所有三种类型的*oid 都是相同的;* 仅有*不同*之处。

下表描述了常规 Oid、直接 Oid 和同步 Oid 之间的差异。

| | 常规 OID | 直接 OID | 同步 OID |
| --- | --- | --- | --- |
| 有效负载 | [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) | NDIS_OID_REQUEST | NDIS_OID_REQUEST |
| OID 类型 | Stats、Query、Set、Method | Stats、Query、Set、Method | Stats、Query、Set、Method |
| 可以通过 | 协议，筛选器 | 协议，筛选器 | 协议，筛选器 |
| 可以通过 | 微型端口，筛选器 | 微型端口，筛选器 | 微型端口，筛选器 |
| 筛选器可以修改 | “是” | “是” | “是” |
| NDIS 分配内存 | 对于每个筛选器（OID 克隆） | 对于每个筛选器（OID 克隆） | 仅当大量筛选器（调用上下文）时 |
| 可以挂起 | “是” | “是” | 无 |
| 可以阻止 | “是” | 无 | 无 |
| IRQL | = = 被动 | \<= 调度 | \<= 调度 |
| [由 NDIS 序列化](miniport-adapter-oid-request-serialization.md) | “是” | 无 | 无 |
| 调用筛选器 | 式 | 式 | 反复 |
| 筛选器克隆 OID | “是” | “是” | 无 |

## <a name="filtering"></a>筛选

与其他两种 OID 调用一样，筛选器驱动程序可以在同步调用中完全控制 OID 请求。 筛选器驱动程序可以观察、截获、修改和颁发同步 Oid。 不过，为了提高效率，同步 OID 的机制略有不同。

### <a name="passthrough-interception-and-origination"></a>传递、拦截和发放

从概念上讲，所有 OID 请求都是从较高的驱动程序发出的，并由较低的驱动程序完成。 在此过程中，OID 请求可能会传递任意数量的筛选器驱动程序。

在最常见的情况下，协议驱动程序发出 OID 请求，所有筛选器只是向下传递 OID 请求，而不进行修改。 下图说明了此常见方案。

![典型的 OID 路径源自协议](images/synchronous_oids_oid_path_full.png "典型的 OID 路径源自协议")

但是，任何筛选器模块都允许截获 OID 请求并完成它。 在这种情况下，请求不会传递到较低的驱动程序，如下图所示。

![典型的 OID 路径源自协议并被筛选器截获](images/synchronous_oids_oid_path_intercepted.png "典型的 OID 路径源自协议并被筛选器截获")

在某些情况下，筛选器模块可能决定发出自己的 OID 请求。 此请求从筛选器模块的级别开始，并只遍历较低的驱动程序，如下图所示。

![典型的 OID 路径源自筛选器](images/synchronous_oids_oid_path_filter_originated.png "典型的 OID 路径源自筛选器")

所有 OID 请求都具有此基本流程：更高的驱动程序（协议或筛选器驱动程序）发出请求，驱动程序（微型端口或筛选器驱动程序）完成了请求。

### <a name="how-regular-and-direct-oid-requests-work"></a>常规和直接 OID 请求的工作方式

定期或直接 OID 请求将以递归方式进行调度。 下图显示了函数调用序列。 请注意，序列本身非常类似于上一节的关系图中所述的顺序，但却排列为显示请求的递归特性。

![常规和直接 OID 请求的函数调用序列](images/synchronous_oids_regular_oid_request_sequence.png "常规和直接 OID 请求的函数调用序列")

如果安装了足够的筛选器，则将强制 NDIS 分配新的线程堆栈，使递归更深层。

NDIS 将[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构视为只对堆栈中的单个跃点有效。 如果筛选器驱动程序要将请求传递给下一个较低的驱动程序（这就是大多数 Oid 的情况），则筛选器驱动程序*必须*插入数个数十行的样板代码以克隆 OID 请求。 此样板有几个问题：

1. 它强制内存分配克隆 OID。 命中内存池的速度很慢，因而无法保证 OID 请求的转发进度。
2. 由于所有筛选器驱动程序都将 NDIS_OID_REQUEST 的内容复制到另一个，因此 OID 结构设计必须在一段时间内保持不变。
3. 需要如此多的样本来掩盖筛选器实际执行的操作。

### <a name="the-filtering-model-for-synchronous-oid-requests"></a>同步 OID 请求的筛选模型

同步 OID 请求的筛选模型利用调用的同步特性来解决上一部分中所述的问题。

#### <a name="issue-and-complete-handlers"></a>问题和完成处理程序

与常规和直接 OID 请求不同，同步 OID 请求有两个筛选器挂钩：问题处理程序和完整处理程序。 筛选器驱动程序既可以注册，也可以注册两个挂钩。

为每个筛选器驱动程序调用发出调用，从堆栈顶部向下到堆栈的底部。 任何筛选器的问题调用都可以使 OID 停止，并通过某些状态代码完成 OID。 如果没有任何筛选器决定截获 OID，则 OID 将达到 NIC 驱动程序，该驱动程序必须以同步方式完成 OID。

完成 OID 后，将为每个筛选器驱动程序调用完整调用，从堆栈中的任意位置开始，直到堆栈的顶部。 完整调用可以检查或修改 OID 请求，并检查或修改 OID 的完成状态代码。

下图说明了典型的情况，即协议发出同步 OID 请求，筛选器不截获请求。

![同步 OID 请求的函数调用序列](images/synchronous_oids_synchronous_oid_request_sequence.png "同步 OID 请求的函数调用序列")

请注意，同步 Oid 的调用模型是迭代的。 这可保持堆栈的使用界限，从而无需再展开堆栈。

如果筛选器驱动程序在其问题处理程序中截获了同步 OID，则不会为较低级别的筛选器或 NIC 驱动程序提供 OID。 但是，仍会调用更高筛选器的完整处理程序，如下图所示：

![通过筛选器截获同步 OID 请求的函数调用序列](images/synchronous_oids_synchronous_oid_request_sequence_intercepted.png "通过筛选器截获同步 OID 请求的函数调用序列")

#### <a name="minimal-memory-allocations"></a>最小内存分配

常规和直接 OID 请求要求使用筛选器驱动程序来克隆 NDIS_OID_REQUEST。 相反，不允许克隆同步 OID 请求。 此设计的优势在于，同步 Oid 的延迟较低–当 OID 在筛选器堆栈下向下移动时，OID 请求不会反复克隆–并且失败的机会更少。

但是，这会引发新问题。 如果无法克隆 OID，筛选器驱动程序将存储其每个请求的状态？ 例如，假设筛选器驱动程序将一个 OID 转换为另一个 OID。 在堆栈中，筛选器需要保存旧 OID。 在备份堆栈的方式上，筛选器需要还原旧 OID。

为了解决此问题，NDIS 为每个正在进行的同步 OID 请求分配每个筛选器驱动程序的指针大小的槽。 NDIS 将来自筛选器的问题处理程序的调用中的此槽保存到其完整处理程序。 这样，就可以使问题处理程序保存关闭状态，该状态稍后由整个处理程序使用。 下面的代码片段演示了一个示例。

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

NDIS 每次调用为每个筛选器保存一个 PVOID。 NDIS 试探性地在堆栈上分配了合理数量的槽，因此在常见情况下有零个池分配。 这通常不超过七个筛选器。 如果用户设置了反常的情况，NDIS 会回退到池分配。

#### <a name="reduced-boilerplate"></a>样本减少

请考虑[示例样板上用于处理常规或直接 OID 请求](example-boilerplate-for-handling-regular-or-direct-oid-requests.md)的样本。 该代码只是注册 OID 处理程序的输入成本。 如果您想要颁发自己的 Oid，则必须再添加十二行样板。 对于同步 Oid，无需额外的复杂操作来处理异步完成。 因此，您可以大致了解这种样板。

下面是使用同步 Oid 的最小颁发处理程序：

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

如果要截获或修改特定 OID，只需添加几行代码即可完成此操作。 最小的完成处理程序甚至更简单：

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

同样，筛选器驱动程序只需使用一行代码，就可以发出自己的新同步 OID 请求：

```cpp
status = NdisFSynchronousOidRequest(binding->NdisBindingHandle, &oid);
```

与此相反，需要发出常规或直接 OID 的筛选器驱动程序必须设置一个异步完成处理程序，并实现一些代码，以便将其自己的 OID 完成与刚刚克隆的 Oid 的完成区分开来。 下面是[有关发出常规 OID 请求的示例样板](example-boilerplate-for-issuing-a-regular-oid-request.md)的示例。

## <a name="interoperability"></a>互操作性

尽管常规的、直接的和同步调用样式均使用相同的数据结构，但管道并不会跳到小型小型中的同一处理程序。 此外，某些 Oid 不能用于某些管道。 例如， [OID_PNP_SET_POWER](oid-pnp-set-power.md)需要小心同步，并经常强制微型端口发出阻止调用。 这使得在直接 OID 回调中难以处理它，并阻止其在同步 OID 回调中使用。 

因此，与直接 OID 请求一样，同步 OID 调用只能与 Oid 的子集一起使用。 在 Windows 10 版本1709中，同步 OID 路径仅支持[接收方缩放版本2（RSSv2）](receive-side-scaling-version-2-rssv2-.md)中使用的[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID。

## <a name="implementing-synchronous-oid-requests"></a>实现同步 OID 请求

有关在驱动程序中实现同步 OID 请求接口的详细信息，请参阅以下主题：

- [微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)
- [筛选器模块 OID 请求](filter-module-oid-requests.md)
- [协议驱动程序 OID 请求](protocol-driver-oid-requests.md)

