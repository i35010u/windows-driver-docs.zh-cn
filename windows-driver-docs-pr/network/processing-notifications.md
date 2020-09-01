---
title: 处理通知
description: 处理通知
ms.assetid: f3e97d23-b463-4c3b-822d-b911f6fbe00e
keywords:
- 通知对象 WDK 网络，处理通知
- 网络通知对象 WDK，处理通知
- 通知 WDK 网络，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21db5ff7a1adc012970312d20fb50299ef485195
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215194"
---
# <a name="processing-notifications"></a>处理通知





网络配置子系统发送通知以按下列间隔通知对象：

-   在网络设置过程中（包括操作系统安装）在以前不支持网络的操作系统上安装网络功能、升级操作系统或卸载网络功能

-   在网络配置过程中--包括添加、删除、启用和禁用网络组件、更改网络组件以及更改网络配置子系统将网络组件绑定到一起的方式

-   应用程序指示子系统显示拥有通知对象的网络组件的属性之后

为了处理通知，notify 对象会执行以下常规操作顺序：

1.  加载 "通知" 对象时，它将读取系统注册表，以在其内部数据结构中形成当前网络配置的模型。

2.  网络配置子系统将通知发送到通知对象，告知通知对象之前请求的网络更改，通知对象会修改其内部数据结构以跟踪这些更改。

3.  当网络配置子系统完成将通知发送到 notify 对象时，子系统将调用 notify 对象的 [**INetCfgComponentControl：： ApplyRegistryChanges**](/previous-versions/windows/hardware/network/ff547727(v=vs.85)) 方法来提交对系统注册表所做的更改。

**注意**   上述序列中提到的通知还可以包括对 notify 对象的[**INetCfgComponentControl：： CancelChanges**](/previous-versions/windows/hardware/network/ff547728(v=vs.85))方法的调用，在这种情况下，notify 对象应恢复为原始网络配置。
在修改原始网络配置之前，notify 对象应创建两个配置副本。 Notify 对象可以修改一个副本以包含更改，并将另一个副本保留在原始状态。 当恢复到原始网络配置时，通知对象可以使用未修改的副本。

 

 

