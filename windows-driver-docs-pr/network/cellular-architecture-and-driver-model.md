---
title: 手机网络体系结构和实现
description: 适用于 Windows 10 的移动电话网络体系结构包含 Windows 8.1 和 Windows Phone 8.1 中的元素。
ms.assetid: A6F23D12-BCF0-496A-B881-C1F6B35EDA4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddccf6beed7f381f52ed29c9a02f4bb18325d66d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562120"
---
# <a name="cellular-architecture-and-implementation"></a>手机网络体系结构和实现


适用于 Windows 10 的移动电话网络体系结构包含 Windows 8.1 和 Windows Phone 8.1 中的元素。 下面是有关比较，以及新的 Windows 10 体系结构关系图和必须实现的移动电话网络组件的 Windows 8.1 和 Windows Phone 8.1 移动电话网络体系结构关系图。

## <a name="windows10-architecture"></a>Windows 10 体系结构：


![windows 10 手机网络体系结构](images/win10-cellular-architecture.png)

## <a name="windows10-cellular-implementation-requirements"></a>Windows 10 手机的实现要求


适用于 Windows 10，必须实现的移动电话网络组件取决于该设备是否使用 Windows 10 桌面版或 Windows 10 移动版。

对于桌面版本的 Windows 10，需要以下各项。

-   在您的调制解调器的硬件中实现 MBIM 协议接口。
-   实现到调制解调器硬件 USB 接口。 它可能是可移动的 USB 硬件保护装置或将自己呈现为 USB 主控制器的另一个接口。

Windows 10 移动版，需要满足以下条件：

- 实现 IHV RIL （单选接口层） 和调制解调器硬件的移动宽带 NDIS 驱动程序。
  ## <a name="windows-81-architecture"></a>Windows 8.1 体系结构：


![windows 8.1 手机网络体系结构](images/win81-cellular-architecture.png)

## <a name="windows-phone-81-architecture"></a>Windows Phone 8.1 体系结构：


![windows phone 8.1 移动电话网络体系结构](images/winphone81-cellular-architecture.png)


## <a name="related-topics"></a>相关主题


[移动宽带 (MB) 设计指南](mobile-broadband--mb--design-guide.md)

 

 






