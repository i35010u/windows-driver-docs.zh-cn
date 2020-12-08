---
title: 更改跟踪会话的属性
description: 更改跟踪会话的属性
keywords:
- 跟踪会话 WDK，属性
- 属性 WDK TraceView
- 可变属性 WDK TraceView
- 显示跟踪会话属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcecc4f91d865066a227a6de4934449f2b97a814
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784053"
---
# <a name="changing-the-properties-of-a-trace-session"></a>更改跟踪会话的属性


在运行会话时，可以更改跟踪会话的选定属性。 你还可以在会话运行时更改跟踪提供程序的 [跟踪标志](trace-flags.md) 和 [跟踪级别](trace-level.md) 属性。

### <a name="span-iddisplay_the_propertiesspanspan-iddisplay_the_propertiesspandisplay-the-properties"></a><span id="display_the_properties"></span><span id="DISPLAY_THE_PROPERTIES"></span>显示属性

" [跟踪会话" 列表](trace-session-list.md) 中的列表示跟踪会话及其提供程序的属性。

若要显示跟踪会话及其提供程序的所有属性，请在 "跟踪会话" 列表中右键单击任意列标题。 此操作显示一个快捷菜单，其中显示了所有可用列。 选中的列显示在 "跟踪会话" 列表中，未选中的列将隐藏。 若要显示或隐藏 "跟踪会话" 列表中的列，请在快捷菜单中单击 "列名称"。

若要将列配置保存为未来 TraceView 会话的默认值，请右键单击 "跟踪会话" 列表中的任何列标题，然后单击 " **另存为默认值**"。

### <a name="span-idfind_changeable_propertiesspanspan-idfind_changeable_propertiesspanfind-changeable-properties"></a><span id="find_changeable_properties"></span><span id="FIND_CHANGEABLE_PROPERTIES"></span>查找可更改属性

" [跟踪会话" 列表](trace-session-list.md) 中的列表示跟踪会话及其跟踪提供程序的属性。

对于正在运行的跟踪会话，运行跟踪会话时可更改的属性显示可用。 仅当停止跟踪会话时才可以更改的属性将显示为灰色。 无法更改跟踪日志中跟踪消息的属性。

### <a name="span-idchange_a_propertyspanspan-idchange_a_propertyspanchange-a-property"></a><span id="change_a_property"></span><span id="CHANGE_A_PROPERTY"></span>更改属性

若要更改属性的值，请单击值，然后在字段中键入新值。 若要保存新值，请单击任何其他单元。

### <a name="span-idset_valuespanspan-idset_valuespanset-value"></a><span id="set_value"></span><span id="SET_VALUE"></span>设置值

" **标志** " 和 " **级别** " 列中的值表示跟踪会话中跟踪提供程序的 [跟踪标志](trace-flags.md) 和 [跟踪级别](trace-level.md) 属性。 " **标志** " 和 " **级别** " 列中的值可以是一个十六进制值，该值表示实际值或 "SET" 一词。

" **集** " 的值指示在 " **跟踪标志和级别选择** " 对话框中设置跟踪标志和跟踪级别。 若要打开 " **跟踪标志和级别选择** " 对话框，请单击 **设置** 值。

 

 





