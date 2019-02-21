---
title: 测试的传感器数据检索
description: 传感器诊断工具，可以通过调用传感器 API 中的属性来测试您的数据检索的驱动程序和固件支持。
ms.assetid: A4473253-D4AC-4374-9C5D-919B597FE2F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4d898ff9b4c5983cf4321671cc6fc4460057d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519771"
---
# <a name="testing-sensor-data-retrieval"></a>测试的传感器数据检索


传感器诊断工具，可以通过调用传感器 API 中的属性来测试您的数据检索的驱动程序和固件支持。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-retrieve-a-single-sensor-reading"></a>配置传感器诊断工具来检索单个传感器读数


以下过程介绍如何配置诊断的工具，以检索读取加速感应器。

1.  展开左侧的传感器窗格中加速感应器的节点。 检查**已连接**框，并取消选中**已订阅**框。
2.  旋转加速感应器和固定的。
3.  单击**刷新数据/执行**按钮，然后查看右窗格中的 Data 节中检索到的数据。

右窗格中的数据部分包含有关您的传感器更新后的数据。 此数据应对应于加速感应器的静态位置。

## <a name="configuring-the-sensor-diagnostic-tool-for-synchronous-polling"></a>配置传感器诊断工具的同步轮询


以下过程介绍如何配置诊断的工具进行同步的加速感应器轮询。 换而言之，这允许你以获取在固定时间间隔从传感器读取数据。

1.  展开的节点，在左侧的传感器窗格中; 加速感应器检查**已连接**框，并取消选中**已订阅**框。
2.  在中**自动数据请求**文本框中，输入所需的轮询间隔以毫秒为单位。 （请注意，间隔为零会禁用同步轮询）。

右窗格中的数据部分将开始显示轮询的数据。 移动加速感应器，你应该看到此窗格中的新值。

CSV 文件中，可以记录轮询的传感器数据。 请参阅[测试传感器事件](testing-sensor-events.md)主题以及有关如何执行此操作的说明的"日志记录事件数据的 CSV 文件"部分。

您可以指定哪些数据应与该工具的 Data 节中显示**Datafield**将出现在第二行的右窗格中的控件的下拉列表。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试传感器属性支持](testing-and-logging-sensor-data.md)  
[传感器的测试活动](testing-sensor-events.md)  



