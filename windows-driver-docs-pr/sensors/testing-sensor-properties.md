---
title: 测试传感器数据检索
description: 传感器诊断工具允许通过在传感器 API 中调用属性来测试驱动程序和固件支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64e624ce549aee6075661f6bb155979b201acca8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805055"
---
# <a name="testing-sensor-data-retrieval"></a>测试传感器数据检索


传感器诊断工具允许通过在传感器 API 中调用属性来测试驱动程序和固件支持。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-retrieve-a-single-sensor-reading"></a>配置传感器诊断工具以检索单个传感器读数


下面的过程介绍如何配置诊断工具以检索加速感应程序读取。

1.  在左侧传感器窗格中展开加速感应节点。 选中 " **已连接** " 框，并取消选中 "已 **订阅** " 框。
2.  旋转加速感应并固定到位。
3.  单击 " **刷新数据"/"执行** " 按钮，然后在右窗格的 "数据" 部分中查看检索到的数据。

右窗格的 "数据" 部分包含传感器的更新数据。 此数据应与加速感应的静态位置相对应。

## <a name="configuring-the-sensor-diagnostic-tool-for-synchronous-polling"></a>为同步轮询配置传感器诊断工具


下面的过程介绍如何将诊断工具配置为对加速感应程序执行同步轮询。 换句话说，这使您能够定期从传感器读取数据。

1.  在左侧传感器窗格中展开加速感应的节点;选中 " **已连接** " 框，并取消选中 "已 **订阅** " 框。
2.  在 " **自动数据请求** " 文本框中，输入所需的轮询间隔（以毫秒为单位）。  (请注意，间隔为0将禁用同步轮询。 ) 

右窗格的 "数据" 部分将开始显示轮询后的数据。 移动加速感应时，应会在此窗格中看到新值。

可以在 CSV 文件中记录轮询的传感器数据。 有关如何执行此操作的说明，请参阅 [测试传感器事件](testing-sensor-events.md) 主题和 "将事件数据记录到 CSV 文件" 一节。

可以指定应在工具的数据部分中显示的数据，其 " **Datafield** " 下拉列表显示在右窗格中的第二行控件中。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试传感器属性支持](testing-and-logging-sensor-data.md)  
[测试传感器事件](testing-sensor-events.md)  



