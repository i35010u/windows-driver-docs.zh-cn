---
title: 访问 NET_BUFFER_LIST IPsec 卸载版本 2 中的信息
description: 访问 IPsec 卸载版本 2 中的 NET_BUFFER_LIST 信息
ms.assetid: 0c27b594-2c61-4459-96df-1d7445100bc5
keywords:
- IPsecOV2 WDK TCP/IP 传输，NET_BUFFER_LIST 信息
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d7c15eefeb4ae8cdc2c57095a3f457531f29127
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563797"
---
# <a name="accessing-netbufferlist-information-in-ipsec-offload-version-2"></a>访问 NET\_缓冲区\_IPsec 卸载版本 2 中的列表信息

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 提供带外 (OOB) 中的数据**NetBufferListInfo**的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，它指定链接的列表[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 **NetBufferListInfo**成员是包含信息普遍适用于 NET 的所有值的数组\_缓冲区列表中的结构。

使用具有以下标识符[ **NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏来设置和获取 IPsec 卸载版本 2 (IPsecOV2) 中OOB数据**NetBufferListInfo**数组：

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
指定所使用的 IPsecOV2 信息中的 TCP/IP 协议中向 NIC 的 IPsec 任务卸载 当指定**IPsecOffloadV2NetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_IPSEC\_将卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)结构。

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
指定所使用的 IPsecOV2 隧道信息中的 TCP/IP 协议中向 NIC 的 IPsec 任务卸载 当指定**IPsecOffloadV2TunnelNetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_IPSEC\_将卸载\_V2\_隧道\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565843)结构。

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
指定在 IPsec 标头的标头偏移量[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)和下一步的标头和板长度的值。 当指定**IPsecOffloadV2HeaderNetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_IPSEC\_将卸载\_V2\_标头\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565812)结构。

 

 





