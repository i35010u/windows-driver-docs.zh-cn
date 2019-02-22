---
title: NetAdapterCx 客户端驱动程序的关闭序列
description: NetAdapterCx 客户端驱动程序的关闭序列
ms.assetid: 9E16172C-9E45-4ED7-B6D2-7539DF4718B5
keywords:
- NetAdapterCx 客户端驱动程序的关闭序列
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48635d5c7bb5decb13c6a7c69da2f2db7e31ced7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526761"
---
# <a name="power-down-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx 客户端驱动程序的关闭序列

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

下图显示了当关闭 NetAdapterCx 调用客户端驱动程序的事件回调函数的顺序和删除设备。 在序列图顶部开头操作设备处于工作电源状态 (D0):

<img src="images/netadaptercx-powerdown.png" alt="Device enumeration and power-down sequence for NetAdapterCx client driver" title="设备枚举和 NetAdapterCx 客户端驱动程序的关闭序列" style="width: 600px;"/>

广泛的水平线将标记中关闭设备所涉及的步骤。 图左侧列描述相应步骤，并在右侧列列出完成该操作的事件回调。 虽然其他步骤普遍适用于所有基于 WDF 驱动程序，有特定的 NetAdapterCx，标记为蓝色文本的步骤。

如图所示，电源关闭和删除序列涉及框架中调用的函数中导致设备操作所涉及的相反顺序调用相应的"撤消"回调。 框架中删除的设备对象后删除设备对象上下文区域。
