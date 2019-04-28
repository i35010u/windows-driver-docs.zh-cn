---
title: NetworkingInfo
description: NetworkingInfo
ms.assetid: 81c615d4-8a7c-4d28-a3ce-5233899e35cf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba60c6300cfb3c745028c51bc078bbb6a53f777
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346547"
---
# <a name="networkinginfo"></a>NetworkingInfo


架构路径：\\Printer.DeviceInfo:NetworkingInfo

节点类型： 属性

本部分介绍与作为一个整体设备相关联的数据。 用户或管理员可以设置这种数据进行个性化设置其设备。

NetworkingInfo 有两个值：**主机名**并**IPAddress**。

### <a name="span-idhostnamespanspan-idhostnamespan-hostname"></a><span id="hostname"></span><span id="HOSTNAME"></span> HostName

Schema Path:\\Printer.DeviceInfo:NetworkingInfo.HostName

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个字符串，其中包含当前的网络设备的主机名。 此信息可能不可用的所有设备。

### <a name="span-idipaddressspanspan-idipaddressspan-ipaddress"></a><span id="ipaddress"></span><span id="IPADDRESS"></span> IPAddress

Schema Path:\\Printer.DeviceInfo:NetworkingInfo.IPAddress

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个字符串，其中包含当前的 TCP/IP 地址的设备。 此地址可以是 IPV4 或 IPV6 格式。 此地址是端口监视器当前用来与打印设备进行通信的地址。

 

 




