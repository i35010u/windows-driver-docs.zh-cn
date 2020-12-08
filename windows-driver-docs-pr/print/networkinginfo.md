---
title: NetworkingInfo
description: NetworkingInfo
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6223a4dc403e29c9505cea354931592017876a8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807809"
---
# <a name="networkinginfo"></a>NetworkingInfo


架构路径： \\ DeviceInfo： NetworkingInfo

节点类型：属性

本部分处理与设备整体关联的数据。 用户或管理员可以设置大部分数据来个性化其设备。

NetworkingInfo 有两个值： **主机名** 和 **ip 地址**。

### <a name="span-idhostnamespanspan-idhostnamespan-hostname"></a><span id="hostname"></span><span id="HOSTNAME"></span> 段

架构路径： \\ DeviceInfo： NetworkingInfo

节点类型：值

数据类型：双向 \_ 字符串

说明：包含设备当前网络主机名的字符串。 此信息可能不适用于所有设备。

### <a name="span-idipaddressspanspan-idipaddressspan-ipaddress"></a><span id="ipaddress"></span><span id="IPADDRESS"></span> 地址

架构路径： \\ DeviceInfo： NetworkingInfo

节点类型：值

数据类型：双向 \_ 字符串

说明：包含设备当前 TCP/IP 地址的字符串。 此地址可以是 IPV4 格式或 IPV6 格式。 此地址是端口监视器当前用于与打印设备通信的地址。

 

 




