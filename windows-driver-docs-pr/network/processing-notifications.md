---
title: 处理通知
description: 处理通知
ms.assetid: f3e97d23-b463-4c3b-822d-b911f6fbe00e
keywords:
- 通知对象 WDK 网络，处理通知
- 网络通知对象 WDK，处理通知
- 通知 WDK 网络、 处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 611fe10146bda63f712dce90bcf57717edc68ff2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327621"
---
# <a name="processing-notifications"></a>处理通知





网络配置子系统发送通知来通知在以下时间间隔的对象：

-   在网络安装程序-包括操作系统安装，以前不支持网络、 升级操作系统，或卸载网络功能的操作系统上安装网络功能

-   在网络配置-过程包括添加、 删除、 启用，并禁用网络组件、 更改网络组件和更改网络配置子系统一起绑定的网络组件如何

-   应用程序指示要显示的子系统之后，它自己的网络组件的属性通知对象

若要处理通知，通知对象，请执行以下常规顺序操作：

1.  加载时通知对象，它会读取系统注册表，以形成在其内部数据结构中当前的网络配置的模型。

2.  网络配置子系统将通知发送到网络更改有关的通知对象，后通知以前所请求的对象，该通知对象修改其内部数据结构来跟踪这些更改。

3.  子系统的网络配置子系统完成通知发送到通知对象操作后，调用通知对象的[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547727)方法将更改提交到系统注册表。

**请注意**  上述顺序中所述的通知还可以包括对通知对象的调用[ **INetCfgComponentControl::CancelChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff547728)中的方法这种情况下通知对象应还原为原始的网络配置。
在修改之前的原始网络配置，通知对象应进行配置的两个副本。 通知对象可以修改包括更改并将另一副本保留在原始条件中的一个副本。 恢复到原始的网络配置时，通知对象可以使用未修改的副本。

 

 

 





