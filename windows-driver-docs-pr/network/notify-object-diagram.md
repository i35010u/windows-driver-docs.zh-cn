---
title: 通知对象关系图
description: 通知对象关系图
ms.assetid: d7c177c0-2dc6-47ed-97fb-5c87cbbc8d6f
keywords:
- 通知对象 WDK 网络、 关系图
- 网络通知对象 WDK，关系图
- 网络配置子系统 WDK
- 子系统 WDK 网络配置
- 通知 WDK 网络 notifyo 对象关系图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19400588f135802f22639ec9488ca415b3559439
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533402"
---
# <a name="notify-object-diagram"></a>通知对象关系图





下图显示了如何安装或控制网络调用的客户端应用程序*网络配置子系统*。 此子系统调用网络类安装程序来安装网络组件并注册通知这些组件的对象。 通知子系统返回到的对象调用以配置代表那些组件拥有的对象，这些网络。

![关系图说明如何安装或控制网络的客户端应用程序调用的网络配置子系统](images/netcfg.png)

 

 





