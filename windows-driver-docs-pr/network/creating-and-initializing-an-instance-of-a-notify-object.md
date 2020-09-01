---
title: 创建和初始化通知对象的实例
description: 创建和初始化通知对象的实例
ms.assetid: 933d24cc-d1a0-4768-9bba-4c78150a84da
keywords:
- 通知对象 WDK 网络，实例
- 网络通知对象 WDK，实例
- 通知对象的实例 WDK 网络
- 正在初始化通知对象实例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9cee7d9516b8bbfeb0a00ce38d39717e1f643b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210207"
---
# <a name="creating-and-initializing-an-instance-of-a-notify-object"></a>创建和初始化通知对象的实例





网络配置子系统必须创建通知对象的实例并初始化对象，子系统才能通知通知对象对网络配置所做的更改并显示拥有该对象的组件的自定义属性页。

子系统从 DLL 的类工厂创建通知对象的实例。 然后，类工厂为 notify 类调用构造函数。

类构造函数应首先向类数据成员赋值。 构造函数最初分配的值包括：

-   构造函数应将指向网络组件 [**INetCfgComponent**](/previous-versions/windows/hardware/network/ff547715(v=vs.85))的实例的接口指针设置为 **NULL** 值。

-   构造函数应将指向网络配置对象 [**INetCfg**](/previous-versions/windows/hardware/network/ff547694(v=vs.85))实例的接口指针设置为 **NULL** 值。

-   构造函数应将指定通知对象之前执行的操作的变量设置为标识未知操作的常数。 有关此变量的详细信息，请参阅 [定义通知类](defining-a-notify-class.md)。

网络配置子系统创建 notify 对象的实例后，子系统将调用对象的 [**INetCfgComponentControl：： initialize**](/previous-versions/windows/hardware/network/ff547729(v=vs.85)) 方法来初始化对象实例。 在此调用中，子系统传递 **INetCfgComponent** 接口指针。 此 **INetCfgComponent** 向通知对象提供对象的组件的实例，该实例可供对象用于访问和控制组件。 在此调用中，子系统还会传递 **INetCfg** 接口指针，以提供通知对象，其中包含通知对象用于访问网络配置的所有方面的网络配置对象的实例。

**Initialize**方法应将网络配置子系统提供的**INetCfgComponent**和**INetCfg**接口指针分配给 notify 类的数据成员。 **初始化** 之后，应调用：

-   用于递增网络配置对象的引用计数的 **INetCfg：： AddRef** 方法

-   **INetCfgComponent：： AddRef**方法递增拥有通知对象的组件的引用计数

在 **Initialize** 返回之前，不会调用其他通知对象接口方法。

 

