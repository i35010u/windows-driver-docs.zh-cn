---
title: 丢失和重新获取数据包数据服务
description: 丢失和重新获取数据包数据服务
ms.assetid: 1e9d6c34-f7fc-47e9-aa52-409b9e9ff4f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193810084e1648ec7274f8b4b88a1e45f2af2df4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523384"
---
# <a name="losing-and-regaining-packet-data-service"></a>丢失和重新获取数据包数据服务


下图显示了过程时，他们会失去不同的时间间隔的信号强度和数据包服务应遵循微型端口驱动程序。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明丢失和重新获取信号数据包数据服务的关系图](images/wwanregainingpacketdataservice.png)

若要重新获得数据包数据服务后已丢失，使用以下过程：

1.  微型端口驱动程序将发送 NDIS\_WWAN\_链接\_MB 服务的状态。

2.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567931)到 MB 服务。

3.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567931)到 MB 服务。

4.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567931)到 MB 服务。

5.  微型端口驱动程序将发送 NDIS\_WWAN\_注册\_MB 服务的状态。

6.  微型端口驱动程序发送[ **NDIS\_状态\_WWAN\_数据包\_服务**](https://msdn.microsoft.com/library/windows/hardware/ff567850)到 MB 服务。

7.  微型端口驱动程序发送[ **NDIS\_状态\_链接\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567391)到 MB 服务。

8.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567931)到 MB 服务。

 

 





