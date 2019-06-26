---
title: 创建和初始化通知对象的实例
description: 创建和初始化通知对象的实例
ms.assetid: 933d24cc-d1a0-4768-9bba-4c78150a84da
keywords:
- 通知对象 WDK 网络的实例
- 网络通知 WDK，对象的实例
- 通知对象 WDK 网络的实例
- 初始化通知对象实例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ca7f07175d777f389a48d682698d6b7aeb1a5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374919"
---
# <a name="creating-and-initializing-an-instance-of-a-notify-object"></a>创建和初始化通知对象的实例





网络配置子系统必须创建通知对象的实例并初始化该对象之前子系统可以通知的通知对象更改网络配置和显示拥有该组件的自定义属性页对象。

子系统从 DLL 的类工厂创建通知对象的实例。 类工厂然后调用通知类的构造函数。

类构造函数应首先将初始值分配给类数据成员。 构造函数应最初分配的值包括：

-   构造函数应设置为实例的网络组件的接口指针[ **INetCfgComponent**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547715(v=vs.85))到**NULL**值。

-   构造函数应设置为网络配置对象的实例的接口指针[ **INetCfg**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547694(v=vs.85))到**NULL**值。

-   构造函数应设置指定为一个常量，它标识一个未知的操作通知对象以前执行的操作的变量。 有关此变量的详细信息，请参阅[定义通知类](defining-a-notify-class.md)。

子系统的网络配置子系统创建通知对象的实例之后，调用对象的[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))方法来初始化对象实例。 在此调用，传递子系统**INetCfgComponent**接口指针。 这**INetCfgComponent**通知对象提供该对象可用于访问和控制该组件的对象的组件的实例。 在此调用中，子系统还会传递**INetCfg**接口指针，以提供与通知对象用于访问网络配置的所有方面的网络配置对象的实例的通知对象。

**初始化**方法应分配**INetCfgComponent**并**INetCfg**接口提供的网络配置子系统的数据成员的指针通知类。 **初始化**然后应调用：

-   **INetCfg::AddRef**方法来增加网络配置对象的引用计数

-   **INetCfgComponent::AddRef**方法来增加该通知对象所属的组件的引用计数

没有其他通知对象接口的方法调用直到**初始化**返回。

 

 





