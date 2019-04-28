---
title: 测试传感器事件
description: 传感器诊断工具，可以在驱动程序和固件中测试对事件的支持。
ms.assetid: 92C067E0-3787-441E-8A2D-C48367ECE471
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 726aa3f25c3481877d79908126cf484e1aff8e68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354563"
---
# <a name="testing-sensor-events"></a>测试传感器事件


传感器诊断工具，可以在驱动程序和固件中测试对事件的支持。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-capture-event-data"></a>配置传感器诊断工具，用于捕获事件数据


以下过程介绍如何配置诊断的工具，用于捕获事件的加速感应器。

1.  展开左侧的传感器窗格中加速感应器的节点，并确保这两**已连接**并**已订阅**框被选中。
2.  在中**事件**菜单上，确认**显示事件**检查。
3.  在左窗格中选择的加速感应器节点。
4.  旋转设备，并在右窗格中查看事件数据。

下图显示了工具，它开始捕获加速感应器事件后。

![传感器诊断工具： 捕获加速感应器事件](images/sdt-events.png)


## <a name="logging-event-data-to-an-xml-file"></a>事件数据的日志记录到 XML 文件


有你将想要将你的设备的事件数据记录到文件而不是该工具的数据窗格的实例。 如果这是有必要，请执行以下步骤。

1.  配置传感器诊断工具，用于捕获事件数据 （请参阅本主题中的第一个部分。）
2.  在中**事件**菜单中，选择**日志事件**菜单选项。
3.  在出现的对话框，指定日志文件和其位置的名称。
4.  开始测试你的设备。 例如，如果是加速感应器，将开始旋转或移动，传感器。

你的数据将记录到在步骤 3 中指定的文件。 CSV 日志记录启用的事件和数据检索时的事件，仅支持 XML 日志记录。

## <a name="logging-event-data-to-a-csv-file"></a>日志记录事件数据的 CSV 文件


除了传感器数据以 XML 形式的日志记录，你还可以记录该 CSV 文件中。 如果这是有必要，请执行以下步骤。 

> [!NOTE]
> 您可能需要为此管理员身份才能正常运行程序。

1.  配置传感器诊断工具，用于捕获事件数据 （请参阅本主题中的第一个部分。）
2.  在中**传感器**菜单中，选择**启用 CSV 日志记录**菜单选项。
3.  开始测试你的设备。 例如，如果是加速感应器，将开始旋转或移动，传感器。
4.  完成测试后，取消选中**启用 CSV 日志记录**菜单选项。 这将停止日志记录，并将数据保存到输出文件。 将文件放置到可执行文件所在的目录。

你的数据将记录到一个或多个 CSV 文件。 如果存在的集合，该工具将创建每个已连接的传感器的文件。 虽然 XML 日志记录仅支持事件的事件和数据检索支持 CSV 日志记录。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试的传感器数据检索](testing-sensor-properties.md)  
[测试传感器属性支持](testing-and-logging-sensor-data.md)  



