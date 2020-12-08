---
title: 测试传感器事件
description: 传感器诊断工具可让你测试对驱动程序和固件中的事件的支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 141ba5c9e9555f38dca4d245c4ed49b65e0d3f82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812127"
---
# <a name="testing-sensor-events"></a>测试传感器事件


传感器诊断工具可让你测试对驱动程序和固件中的事件的支持。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-capture-event-data"></a>配置传感器诊断工具以捕获事件数据


下面的过程介绍如何将诊断工具配置为捕获加速感应程序的事件。

1.  在左传感器窗格中展开加速感应的节点，并确保选中 " **已连接** " 和 "已 **订阅** " 框。
2.  在 " **事件** " 菜单中，验证是否选中了 " **显示事件** "。
3.  选择左窗格中的 "加速感应" 节点。
4.  旋转设备并在右窗格中查看事件数据。

下图显示了在开始捕获加速感应事件之后的工具。

![传感器诊断工具：捕获加速感应事件](images/sdt-events.png)


## <a name="logging-event-data-to-an-xml-file"></a>将事件数据记录到 XML 文件


在某些情况下，你需要将设备的事件数据记录到文件而不是工具的数据窗格中。 如果这是必需的，请执行以下步骤。

1.  配置传感器诊断工具以捕获事件数据 (参阅本主题中的第一部分。 ) 
2.  在 " **事件** " 菜单中，选择 " **日志事件** " 菜单选项。
3.  在出现的对话框中，指定日志文件的名称及其位置。
4.  开始测试你的设备。 例如，如果是加速感应器，开始旋转或移动传感器。

你的数据将记录到你在步骤3中指定的文件。 仅事件支持 XML 日志记录，同时为事件和数据检索启用了 CSV 日志记录。

## <a name="logging-event-data-to-a-csv-file"></a>将事件数据记录到 CSV 文件


除了将传感器数据记录为 XML，还可以将其记录到 CSV 文件中。 如果这是必需的，请执行以下步骤。 

> [!NOTE]
> 你可能需要以管理员身份运行此程序才能正常工作。

1.  配置传感器诊断工具以捕获事件数据 (参阅本主题中的第一部分。 ) 
2.  在 **传感器** 菜单中，选择 " **启用 CSV 日志记录** " 菜单选项。
3.  开始测试你的设备。 例如，如果是加速感应器，开始旋转或移动传感器。
4.  测试完成后，取消选中 " **启用 CSV 日志记录** " 菜单选项。 这会停止记录，并将数据保存到输出文件。 文件放在与可执行文件相同的目录中。

你的数据将记录到一个或多个 CSV 文件中。 如果存在集合，则该工具将为每个连接的传感器创建一个文件。 事件和数据检索都支持 CSV 日志记录，而仅事件支持 XML 日志记录。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试传感器数据检索](testing-sensor-properties.md)  
[测试传感器属性支持](testing-and-logging-sensor-data.md)  



