---
title: ndiskd.netfragment
description: Ndiskd. netfragment 扩展显示 NET_PACKET_FRAGMENT 结构的相关信息。
keywords:
- ndiskd netfragment Windows 调试
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netfragment
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce6530878b1a1d785a7f456877b7f07204315af9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833233"
---
# <a name="ndiskdnetfragment"></a>!ndiskd.netfragment

**！ Ndiskd netfragment** 扩展显示有关 [网络 \_ 数据包 \_ 片段](/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)结构的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf Class extension (Cx) ](../netcx/index.md)。

```console
!ndiskd.netfragment -handle <x> 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 网络 \_ 数据包片段的地址 \_ 。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

**注意**  请参阅 [对象摘要](../netcx/summary-of-netadaptercx-objects.md) ，以查看说明网络 \_ 数据包对象与 NetAdapterCx 中的其他对象的关系的关系图。

若要获取网络数据包的句柄 \_ ，请执行以下步骤：

1. 运行 [**！ ndiskd. get-netadapter**](-ndiskd-netadapter.md) 扩展。
2. 单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3. 单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行 [**！ ndiskd. cxadapter**](-ndiskd-cxadapter.md) 扩展。
4. 输入包含 *-数据路径* 参数的 **！ cxadapter** 命令，以查看 get-netadapter 的数据路径队列。
5. 单击其中一个数据路径队列的句柄。
6. 单击该数据路径队列的环形缓冲区的句柄。
7. 单击环形缓冲区详细信息底部的 "列出所有元素" 链接，查看其包含的元素。
8. 在环形缓冲区的元素列表中，单击其中一个 [网络 \_ 数据包](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet) 对象。

有关此过程中步骤1-4 的详细信息，请参阅 **！ ndiskd. cxadapter** 主题中的示例。 有关此过程的步骤5的详细信息，请参阅《 [**！ ndiskd. netqueue**](-ndiskd-netqueue.md) 主题中的示例。 有关此过程中步骤6-7 的详细信息，请参阅 [**！ ndiskd. netrb**](-ndiskd-netrb.md) 主题中的示例。 有关此过程步骤8的详细信息，请参阅《 [**！ ndiskd. netpacket**](-ndiskd-netpacket.md) 主题中的示例。
在下面的示例中，查找此网络数据包 ffffd1022d000040 的第一个片段的句柄 \_ 。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

通过单击第一个片段的句柄，或在命令行上输入 **！ ndiskd** 命令，可以查看此网络数据包片段的详细信息 \_ \_ ，包括其虚拟地址、容量以及是否是网络数据包链中的最后一个数据包 \_ 。

```console
0: kd> !ndiskd.netfragment ffffd1022d000040

    NET_PACKET_FRAGMENT ffffd1022d000040

    Virtual Address    ffffd102303e82f8
    Capacity           0n92
    Valid Length       0n34
    Offset             0n58

    Last packet of chain
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[对象摘要](../netcx/summary-of-netadaptercx-objects.md)

[网络 \_ 数据包 \_ 片段](/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)

[网络 \_ 数据包](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
