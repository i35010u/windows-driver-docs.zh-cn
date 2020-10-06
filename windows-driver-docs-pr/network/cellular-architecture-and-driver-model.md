---
title: 手机网络体系结构和实现
description: 适用于 Windows 10 的移动通信体系结构包含来自 Windows 8.1 和 Windows Phone 8.1 的元素。
ms.assetid: A6F23D12-BCF0-496A-B881-C1F6B35EDA4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97ecc5c9fea4ba9169cdedbaa079c4a1ad4fbbb4
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91754886"
---
# <a name="cellular-architecture-and-implementation"></a>手机网络体系结构和实现


适用于 Windows 10 的移动通信体系结构包含来自 Windows 8.1 和 Windows Phone 8.1 的元素。 下面是用于比较的 Windows 8.1 和 Windows Phone 8.1 移动架构关系图，以及新的 Windows 10 体系结构关系图和必须实现的移动电话组件。

## <a name="windows10-architecture"></a>Windows 10 体系结构：


![windows 10 移动电话体系结构](images/win10-cellular-architecture.png)

## <a name="windows10-cellular-implementation-requirements"></a>Windows 10 移动电话实现要求


对于 Windows 10，必须实现的移动电话组件取决于设备使用的是适用于桌面版还是 Windows 10 移动版的 Windows 10。

对于桌面版的 Windows 10，需要满足以下要求。

-   在调制解调器硬件中实现 MBIM 协议接口。
-   对调制解调器硬件实现 USB 接口。 它可以是可移动的 USB 转换器或其他表现为 USB 主机控制器的接口。

对于 Windows 10 移动版，需要满足以下要求：

- 为调制解调器硬件实现 IHV RIL (无线电接口层) 和移动宽带 NDIS 驱动程序。
  ## <a name="windows-81-architecture"></a>Windows 8.1 体系结构：


![windows 8.1 蜂窝体系结构](images/win81-cellular-architecture.png)

## <a name="windows-phone-81-architecture"></a>Windows Phone 8.1 体系结构：


![windows phone 8.1 蜂窝体系结构](images/winphone81-cellular-architecture.png)


 

 






