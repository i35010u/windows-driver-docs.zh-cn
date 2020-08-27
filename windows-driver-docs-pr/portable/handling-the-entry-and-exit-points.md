---
description: 处理入口和出口点
title: 处理入口和出口点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 271116080b44683e641c344f62de2ea3bf5057d0
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968790"
---
# <a name="handling-the-entry-and-exit-points"></a>处理入口和出口点


每次将设备加载到驱动程序的主机进程时，用户模式驱动程序框架 (UMDF) 添加设备对象。 而且，每次框架添加对象时，它都会调用 **IDriverEntry** 接口中的方法。 这些方法可在 CDriver 类中找到。 下表描述了此类中的方法。

| 方法                           | 说明                            |
|----------------------------------|----------------------------------------|
| **IDriverEntry::OnDeinitialize** | 执行必要的清理操作。 |
| **IDriverEntry::OnDeviceAdd**    | 向系统中添加新设备。       |
| **IDriverEntry：： OnInitialize**   | 处理驱动程序初始化。         |

 

在 WpdHelloWorldDriver 中， **OnDeviceAdd** 方法是执行有意义的工作的唯一方法; **OnInitialize** 方法只返回 S \_ OK， **OnDeinitialize** 方法不返回值。

**OnDeviceAdd**方法的代码完成了以下步骤：

1.  创建设备回调对象。
2.  创建 WDF 设备。
3.  创建 WpdBaseDriver 对象并将其分配给 WDF 设备对象。
4.  创建队列回调对象。
5.  创建默认队列。

CDriver 还实现了 **IObjectCleanup：： OnCleanup**，其中包含的代码用于释放对 WpdBaseDriver 对象的引用，该对象由 WDF 设备对象在 **OnDeviceAdd**期间持有。

有关每个接口及其方法的详细信息，请参阅 [UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678) 文档。

 

 




