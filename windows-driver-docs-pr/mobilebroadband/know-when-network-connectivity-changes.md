---
title: 了解网络连接发生更改时
description: 了解网络连接发生更改时
ms.assetid: 2937ba62-16ad-4a81-92e8-62a8bb40d608
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2108c211cedb431d3f76b2a3eb19f993a8997813
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534025"
---
# <a name="know-when-network-connectivity-changes"></a>了解网络连接发生更改时


若要了解何时在网络连接更改，使用[ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)的事件[ **MobileBroadbandAccountWatcher**](https://msdn.microsoft.com/library/windows/apps/hh770597):

1.  实例化[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)对象。

2.  添加[ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)事件处理程序。

3.  调用[**启动**](https://msdn.microsoft.com/library/windows/apps/hh770604)上观察程序。

4.  查询[ **HasNetworkChanged** ](https://msdn.microsoft.com/library/windows/apps/hh770595)属性[ **MobileBroadbandAccountUpdatedEventArgs** ](https://msdn.microsoft.com/library/windows/apps/hh770593)对象中[**AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)事件处理程序。

5.  如果在网络发生了变化，查询[ **CurrentNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770610)当前的网络对象的属性。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






