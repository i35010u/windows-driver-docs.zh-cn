---
title: NetAdapterCx 客户端驱动程序的关闭顺序
description: NetAdapterCx 客户端驱动程序的关闭顺序
ms.assetid: 9E16172C-9E45-4ED7-B6D2-7539DF4718B5
keywords:
- NetAdapterCx 客户端驱动程序的关闭顺序
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5aa3117c75c03162bb715a0538f164600412434e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209011"
---
# <a name="power-down-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx 客户端驱动程序的关闭顺序

下图显示了在关闭和删除设备时，NetAdapterCx 调用客户端驱动程序的事件回调函数的顺序。 序列从图形顶部开始，其操作设备处于工作电源状态（D0）：

<img src="images/netadaptercx-powerdown.png" alt="Device enumeration and power-down sequence for NetAdapterCx client driver" title="NetAdapterCx 客户端驱动程序的设备枚举和关机顺序" style="width: 600px;"/>

大水平行用于标记关闭设备所涉及的步骤。 图左侧的列描述了步骤，右侧的列列出了完成该步骤的事件回调。 用蓝色文本标记的步骤特定于 NetAdapterCx，而其他步骤则适用于所有基于 WDF 的驱动程序。

如图所示，关闭和删除序列涉及到按与使设备正常运行所涉及的函数的相反顺序调用相应的 "撤消" 回调。 框架在删除设备对象上下文区域后删除设备对象。
