---
title: 功能说明
description: 功能说明
ms.assetid: 19c1378d-f8d8-42a2-9776-4f5bfdb9e39e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a41f9de1c6f4954676f3fb2a11a25082ebc76350
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565337"
---
# <a name="feature-description"></a>功能说明


崩溃转储驱动程序提供了新接口以将筛选器驱动程序添加到故障转储堆栈。 此接口不按照任何标准筛选器驱动程序模型。 相反，它公开专有接口，必须使用以便将驱动程序加载到崩溃转储堆栈。

崩溃转储筛选器驱动程序可以通过添加注册表项中的服务名称进行转储堆栈的一部分。 崩溃转储驱动程序加载这些驱动程序时加载的驱动程序转储堆栈中。 筛选器驱动程序加载作为休眠和崩溃转储堆栈的一部分。 这些筛选器驱动程序应提供一系列将休眠和故障转储过程中调用的预定义的回调例程。

筛选模型不允许筛选器驱动程序只能在休眠或崩溃转储堆栈中加载。 服务名称添加到筛选器驱动程序列表后，将在两个堆栈加载列表。 当调用回调例程时，传递参数以指示回调原因。 筛选器驱动程序然后可以确定要执行的操作根据此参数。

 

 




