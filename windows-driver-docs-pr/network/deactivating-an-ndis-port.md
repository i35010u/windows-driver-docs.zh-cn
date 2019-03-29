---
title: 停用 NDIS 端口
description: 停用 NDIS 端口
ms.assetid: 2a5d288f-b6ea-4b63-91a3-44155aae8064
keywords:
- WDK NDIS，停用的端口
- NDIS 端口 WDK，停用
- 停用 NDIS 端口 WDK NDIS
- 停用的即插即用事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06659c1d44b1b038db1da1a56b2cde61a9aad544
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563984"
---
# <a name="deactivating-an-ndis-port"></a>停用 NDIS 端口





若要停用 NDIS 端口，微型端口驱动程序将端口停用插 (PnP) 事件发送到 NDIS。 微型端口驱动程序已成功激活端口后，该驱动程序必须停用该端口，然后它可以释放该端口。 此外，驱动程序可能出于特定于应用程序停用一个端口。 停用，但不能重新激活一个端口，如果释放它后，可以重新激活一个端口。

若要将发送端口停用的即插即用事件，微型端口驱动程序，请使用**NetEventPortDeactivation** PnP 对的调用中的事件代码[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)函数。 若要停用的端口，微型端口驱动程序必须设置的成员[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)结构的*NetPnPEvent*的参数**NdisMNetPnPEvent**指向，如下所示：

<a href="" id="portnumber"></a>**PortNumber**  
事件通知的源端口。 将此成员设置为零，因为在提供的端口号**缓冲区**结构中的成员的**NetPnPEvent**成员指定。

<a href="" id="netpnpevent"></a>**NetPnPEvent**  
一个[ **NET\_PNP\_事件**](https://msdn.microsoft.com/library/windows/hardware/ff568751)描述端口停用事件的结构。 设置此结构的成员，如下所示：

<a href="" id="netevent"></a>**NetEvent**  
一个描述事件的事件代码。 将此成员设置为**NetEventPortDeactivation**。

<a href="" id="buffer"></a>**缓冲区**  
指向数组的 NDIS\_端口\_数字类型的元素。 该数组包含所有微型端口驱动程序正在停用的端口的端口的号。

<a href="" id="bufferlength"></a>**BufferLength**  
中指定的字节数**缓冲区**。 设置**BufferLength**到数组的大小，**缓冲区**指向。 若要获取数组中的元素数，除以中的值**BufferLength** NDIS 的大小\_端口\_数字数据类型。

<a href="" id="other-members"></a>其他成员  
设置网络的其余成员\_PNP\_事件**NULL**。

微型端口驱动程序可以提供一个包含要停用的端口列表的数组。 但是，如果微型端口适配器的默认端口为的目标**NetEventPortDeactivation**即插即用事件，默认端口必须是数组中指定的唯一端口。

微型端口驱动程序可以在任何时候停用活动的端口。 但是，微型端口驱动程序会停用一个端口之前，它必须确保存在没有未完成状态迹象或接收与该端口相关联的迹象。 微型端口驱动程序将发送端口停用的即插即用事件后，它必须不启动任何状态或接收与已停用的端口相关联的迹象。

微型端口驱动程序还可以重新激活一个端口。 有关激活 NDIS 端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

NDIS 时微型端口驱动程序将其停用的端口会绑定到的微型端口驱动程序使用的协议驱动程序的所有通知**NetEventPortDeactivation**即插即用事件。 此即插即用事件将列出这些端口已更改为已分配状态并不包括任何已停用的端口。 有关处理端口停用协议驱动程序中的事件的详细信息，请参阅[处理端口停用的即插即用事件](handling-the-port-deactivation-pnp-event.md)。

该驱动程序微型端口驱动程序分配的 NDIS 端口之前，必须调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)中的属性函数将设置注册[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 微型端口驱动程序可以通过设置 NDIS 控制默认端口的激活\_微型端口\_控件\_默认\_端口属性标志时它们调用**NdisMSetMiniportAttributes**. 如果微型端口驱动程序负责在激活默认端口，并且微型端口驱动程序激活默认端口，它必须先停用的默认端口从返回前[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数。

所有的 NDIS 数组由指定的端口\_端口\_数字元素的数目必须处于激活状态。 微型端口驱动程序不应尝试停用已停用的端口。

NDIS 无法停用端口数组中的任何端口，如果没有任何端口数组中的端口将更改状态。 停用操作会失败，因为某些指定的端口不存在，如果[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)函数将返回 NDIS\_状态\_无效\_端口返回值。 停用操作会失败，因为一些端口未处于激活状态，如果**NdisMNetPnPEvent**返回 NDIS\_状态\_无效\_端口\_状态返回值。

对的调用直到**NdisMNetPnPEvent**返回时，不停用一个端口，并且微型端口驱动程序必须能够处理 OID 请求并发送与该端口相关联的请求。

当微型端口驱动程序会停用的默认端口时，NDIS 会关闭所有基础协议驱动程序和微型端口适配器之间的绑定。 如果尝试停用的默认端口微型端口驱动程序和默认端口已停用[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)失败并返回 NDIS\_状态\_无效\_端口\_状态返回值。 如果尝试停用的默认端口微型端口驱动程序和默认端口不是唯一的 NDIS 数组中指定的端口\_端口\_数字元素**NdisMNetPnPEvent**失败并返回NDIS\_状态\_无效\_端口返回值。 如果微型端口驱动程序设置**缓冲区**成员添加到**NULL**或**BufferLength**为零的成员，NDIS 失败**NdisMNetPnPEvent**调用和返回 NDIS\_状态\_无效\_参数返回值。

端口是成功停用后，端口是已分配状态。 微型端口驱动程序不能指示的状态为已分配状态中的端口或接收的数据。

 

 





