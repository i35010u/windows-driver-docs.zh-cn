---
Description: Handling the Entry and Exit Points
title: 处理入口和出口点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fe426b874ad0f17cac893c3d4508c9a37026bc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568272"
---
# <a name="handling-the-entry-and-exit-points"></a>处理入口和出口点


每次在驱动程序的主机进程中加载设备时用户模式驱动程序框架 (UMDF) 将添加一个设备对象。 并且，每次框架将对象添加时，它会以调用方法**IDriverEntry**接口。 这些方法都位于 CDriver 类。 下表介绍此类中找到的方法。

| 方法                           | 描述                            |
|----------------------------------|----------------------------------------|
| **IDriverEntry::OnDeinitialize** | 执行必要的清理操作。 |
| **IDriverEntry::OnDeviceAdd**    | 将新设备添加到系统。       |
| **IDriverEntry::OnInitialize**   | 处理驱动程序的初始化。         |

 

在 WpdHelloWorldDriver **OnDeviceAdd**方法是执行有意义的工作; 的唯一方法**OnInitialize**方法只需返回 S\_确定和**OnDeinitialize**方法不返回任何值。

代码**OnDeviceAdd**方法完成以下步骤：

1.  创建设备回调对象。
2.  将创建一个 WDF 设备。
3.  创建 WpdBaseDriver 对象并将其分配给 WDF 设备对象。
4.  创建一个队列回调对象。
5.  创建默认的队列。

此外实现了 CDriver **IObjectCleanup::OnCleanup**，其中包含用于发布期间 WDF 设备对象持有 WpdBaseDriver 对象的引用代码**OnDeviceAdd**。

有关每个接口及其方法的详细信息，请参阅[UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678)文档。

 

 




