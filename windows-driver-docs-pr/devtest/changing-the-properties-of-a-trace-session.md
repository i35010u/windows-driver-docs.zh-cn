---
title: 更改跟踪会话的属性
description: 更改跟踪会话的属性
ms.assetid: 6a3522c5-d59b-423b-8d8d-5df9ac3be7cc
keywords:
- 跟踪会话 WDK，属性
- WDK TraceView 属性
- 可更改属性 WDK TraceView
- 显示跟踪会话属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b588c3fc7f838c5ba6420222e51b04475b220991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522774"
---
# <a name="changing-the-properties-of-a-trace-session"></a>更改跟踪会话的属性


运行会话时，可以更改所选的属性的跟踪会话。 此外可以更改[跟踪标志](trace-flags.md)并[跟踪级别](trace-level.md)会话正在运行时跟踪提供程序的属性。

### <a name="span-iddisplaythepropertiesspanspan-iddisplaythepropertiesspandisplay-the-properties"></a><span id="display_the_properties"></span><span id="DISPLAY_THE_PROPERTIES"></span>显示的属性

中的列[跟踪会话列表](trace-session-list.md)表示跟踪会话和其提供程序的属性。

若要跟踪会话列表中显示的跟踪会话和其提供程序，所有属性，请右键单击任意列标题。 此操作会显示快捷菜单，显示所有可用的列。 选中的列会显示在跟踪会话列表和未选中的列隐藏。 若要显示或隐藏某一列在跟踪会话列表中，在快捷菜单中，单击列名称。

要将列配置保存为默认值为将来的 TraceView 会话，请右键单击在跟踪会话列表中，任何列标题，然后单击**另存为默认**。

### <a name="span-idfindchangeablepropertiesspanspan-idfindchangeablepropertiesspanfind-changeable-properties"></a><span id="find_changeable_properties"></span><span id="FIND_CHANGEABLE_PROPERTIES"></span>查找可更改属性

中的列[跟踪会话列表](trace-session-list.md)表示跟踪会话和其跟踪提供程序的属性。

对于正在运行的跟踪会话，显示可用运行跟踪会话时，可以更改的属性。 仅当停止跟踪会话时可以更改的属性会变暗。 不能更改的跟踪日志中跟踪消息的属性。

### <a name="span-idchangeapropertyspanspan-idchangeapropertyspanchange-a-property"></a><span id="change_a_property"></span><span id="CHANGE_A_PROPERTY"></span>更改属性

要更改属性的值，请单击值，然后在字段中键入新值。 若要保存新值，请单击任何其他单元格。

### <a name="span-idsetvaluespanspan-idsetvaluespanset-value"></a><span id="set_value"></span><span id="SET_VALUE"></span>设置值

中的值**标志**并**级别**列表示[跟踪标志](trace-flags.md)并[跟踪级别](trace-level.md)中的跟踪提供程序属性跟踪会话。 中的值**标志**并**级别**列可以是一个十六进制值，表示实际值或 word"的设置"。

值为**设置**指示在中设置的跟踪标志和跟踪级别**跟踪标志和级别选择**对话框。 若要打开**跟踪标志和级别选择**对话框中，单击**设置**值。

 

 





