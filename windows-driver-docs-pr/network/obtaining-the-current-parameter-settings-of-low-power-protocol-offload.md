---
title: 获取当前参数设置的低能耗协议将卸载
description: 获取当前参数设置的低能耗协议将卸载
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 951a7a6ec544544a248b7684b2ede5eb7471f5be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525756"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>获取当前参数设置的低能耗协议将卸载





协议驱动程序可以使用[OID\_PM\_协议\_卸载\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569769)OID 查询以获取所有已卸载的网络适配器上该协议的协议的列表。 从查询中，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指针到一系列[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)描述当前处于活动状态的协议的结构将卸载。 有关的内容信息**NDIS\_PM\_协议\_卸载**结构，请参阅[添加和删除低电源协议卸载](adding-and-deleting-low-power-protocol-offloads.md)。

NDIS 句柄[OID\_PM\_协议\_卸载\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569769)OID 和 GUID\_PM\_协议\_卸载\_列表 WMI代表微型端口驱动程序的请求。 因此，NDIS 微型端口驱动程序不支持所需 OID\_PM\_协议\_卸载\_列表 OID 请求。

过量驱动程序可以使用[OID\_PM\_获取\_协议\_卸载](https://msdn.microsoft.com/library/windows/hardware/ff569766)方法要获取的低能耗协议参数设置的 OID 将卸载从微型端口驱动程序。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构最初包含一个指向协议卸载标识符。 从方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向[**NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构。

 

 





