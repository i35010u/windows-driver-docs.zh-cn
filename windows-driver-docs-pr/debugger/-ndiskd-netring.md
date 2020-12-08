---
title: ndiskd.netring
description: Ndiskd. netring 扩展显示 NET_PACKET_FRAGMENT 结构的相关信息。
keywords:
- ndiskd netring Windows 调试
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 882075726645d5e40272d6d7835f070c67c75eb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833219"
---
# <a name="ndiskdnetring"></a>!ndiskd.netring

**！ Ndiskd netring** 扩展显示有关 [网络 \_ 环](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)结构的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf 类扩展 (Cx) ](../netcx/index.md) 和 [网络环简介](../netcx/introduction-to-net-rings.md)。

```console
!ndiskd.netring -handle <x> [-basic] [-dump]
```

## <a name="parameters"></a>参数

*-handle*   
必需。 NET_RING 的地址

*-基本*    
显示基本信息

*-dump*    
显示有关每个元素的信息

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
6. 单击该数据路径队列的环形缓冲区的句柄。 待定-这是否适用于 netring？
7. 单击环形缓冲区详细信息底部的 "列出所有元素" 链接，查看其包含的元素。 TBD TBD 待定
8. 单击 "网络 \_ 振铃 (集合" ) 对象 TBD。
有关此过程中步骤1-4 的详细信息，请参阅 **！ ndiskd. cxadapter** 主题中的示例。 有关此过程的步骤5的详细信息，请参阅《 [**！ ndiskd. netqueue**](-ndiskd-netqueue.md) 主题中的示例。 有关此过程中步骤6-7 的详细信息，请参阅 [**！ ndiskd. netrb**](-ndiskd-netrb.md) 主题中的示例。 TBD 待定  

在下面的示例中，使用 [**！ ndiskd. cxadapter**](-ndiskd-cxadapter.md) 扩展查找 TBD。

```console
0: kd> !ndiskd.cxdapter 

TBD

TBD

TBD


```

使用 TBD 的地址显示 netring TBD。

```console
0: kd> !ndiskd.netring ffffTBDfffff

TBD

TBD

TBD


```

此示例演示如何使用-dump 选项来显示每个元素的相关信息。

```console
0: kd> !ndiskd.netring ffffTBDfffff -dump

TBD

TBD

TBD

```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[对象摘要](../netcx/summary-of-netadaptercx-objects.md)

[网络 \_ 环](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
