---
title: Windows 筛选平台标注驱动程序简介
description: Windows 筛选平台标注驱动程序简介
ms.assetid: d075da82-8dbc-41a5-a081-dd0e2b292371
keywords:
- Windows 筛选平台标注驱动程序 WDK，有关标注驱动程序
- 有关标注驱动程序的标注驱动程序 WDK Windows 筛选平台，
- 标注 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2eeb7b6039ef79ec6a95dfde477a70020ca6ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519911"
---
# <a name="introduction-to-windows-filtering-platform-callout-drivers"></a>Windows 筛选平台标注驱动程序简介


本部分介绍 Windows 筛选平台[标注驱动程序](callout-driver.md)。 有关 Windows 筛选平台的详细信息，请参阅[Windows 筛选平台](https://go.microsoft.com/fwlink/p/?linkid=90220)Microsoft Windows SDK 中的文档。

### <a name="purpose-of-callout-drivers"></a>标注驱动程序的用途

标注驱动程序实现一个或多个[标注](callout.md)。 标注处理基于 IP 的网络的数据超出了简单的筛选功能的作用域是通过扩展 Windows 筛选平台的功能。 标注通常用于执行以下任务：

<a href="" id="deep-inspection-------"></a>**深度检测**   
复杂的执行检查以确定哪些数据应被阻止，应允许哪些数据，以及哪些数据应传递给另一个筛选器的网络数据。 防病毒产品，例如，可以查找病毒签名。

<a href="" id="packet-modification-------"></a>**数据包修改**   
执行修改和 reinjection 的网络数据包标头和/或数据。 网络地址转换 (NAT) 产品，例如，可以修改 IPv4 数据包的标头。

<a href="" id="stream-modification-------"></a>**Stream 修改**   
在流中执行修改和 reinjection 网络数据。 家长控制产品，例如，无法删除或替换特定的词或短语中的数据流。

<a href="" id="data-logging-------"></a>**数据日志记录**   
网络流量数据的日志。 例如，网络监视产品，可计数由于某种原因丢弃的数据包数。

除了处理网络数据时，标注驱动程序可以执行其他 Windows 筛选平台管理任务，如将筛选器添加到基础筛选引擎。 有关标注驱动程序可以执行其他任务的详细信息，请参阅[调用其他 Windows 筛选平台函数](calling-other-windows-filtering-platform-functions.md)。

 

 





