---
title: 为组件创建属性页
description: 为组件创建属性页
ms.assetid: f353844f-56f4-42cd-8f7d-2fa87f469d3c
keywords:
- 通知对象 WDK 网络，属性页
- 网络通知对象 WDK，属性页
- 属性页 WDK 网络
- 属性 WDK 网络
- 属性页回调函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296014c79cadb493ef68cc0b0d01224323c8dcc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554676"
---
# <a name="creating-property-pages-for-the-component"></a>为组件创建属性页





通知对象后的网络配置子系统调用通知对象的创建自定义属性页[ **INetCfgComponentPropertyUi::MergePropPages** ](https://msdn.microsoft.com/library/windows/hardware/ff547746)方法。 自定义属性页可以合并到组件的属性上的页面的默认集工作表使用**MergePropPages**方法。 **MergePropPages**将返回适当数量的自定义页面可以合并到该值的默认页。

若要创建自定义属性页**MergePropPages**调用 COM **CoTaskMemAlloc**函数分配内存来存放到 PROPSHEETPAGE 结构的句柄。 表示属性页可以创建每个这些句柄。 如果**CoTaskMemAlloc**成功句柄，分配的内存**MergePropPages**将声明并填充**PROPSHEETPAGE**结构的每个属性页。 之后**MergePropPages**填充这些结构，它将调用 Win32 **CreatePropertySheetPage**函数为每个属性页。 在此调用中， **MergePropPages**传递 PROPSHEETPAGE 结构创建的地址。

对于每个属性页，还应实现对话框中的回调函数**MergePropPages**创建。 对话框中的回调函数处理操作系统将发送到与该对话框函数相关联的属性页的消息。 若要将属性页对话框函数与相关联**MergePropPages**应指向**pfnDlgProc**对页的对话框中函数的每个页面每个 PROPSHEETPAGE 结构的成员。

对话框函数处理以下消息：

-   WM\_INITDIALOG 消息，操作系统会显示其关联的属性页之前立即发送给对话框函数。 对话框中的函数通常使用此消息，初始化的属性页以及用于执行任务影响的属性页的外观。

-   WM\_通知消息之后的属性页中发生的事件, 发送到对话框函数。 与此消息一起发送其他信息标识哪些事件已发生。 此事件的信息包含在指向 NMHDR 结构的指针。 NMHDR 属性表可以包含的信息包括，例如：
    -   PSN\_应用事件，指示用户关闭单击确定，或属性页上的应用。 如果用户单击确定，关闭，或应用中，可以调用对话框函数**PropSheet\_Changed**宏以通知属性表页上的信息已更改。 在此调用对话框函数将句柄传递到属性表和页。 对话框函数可以调用 Win32 **GetParent**函数，并将该句柄传递给页后，可以检索到属性表的句柄。

        网络配置子系统对话框函数通知有关更改的属性表后，调用[ **INetCfgComponentPropertyUi::ValidateProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547755)方法来检查所有更改的有效性。 子系统的所有更改都都有效，如果调用通知对象的[ **INetCfgComponentPropertyUi::ApplyProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547741)方法，使所有更改才会生效。 网络配置子系统调用**ApplyProperties**操作系统将关闭对话框的之前。

        **ApplyProperties**可以实现方法，检索用户输入的信息以及可设置到通知对象的数据成员的信息。

    -   PSN\_重置事件，指示操作系统即将销毁属性页。 用户可能要启动此操作的属性页上单击取消。 如果用户单击取消，将调用网络配置子系统[ **INetCfgComponentPropertyUi::CancelProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff547742)方法会导致忽略所有更改。 网络配置子系统调用**CancelProperties**框关闭对话框之前。
    -   PSN\_KILLACTIVE 事件，指示属性页即将变为不活动状态。 当用户激活另一个页面，或单击确定时发生此事件。

*属性页回调*为每个属性页，也可以实现函数**MergePropPages**创建。 属性页的回调函数执行初始化和清理操作的页。 若要将属性页的属性页回调函数，与相关联**MergePropPages**应指向**pfnCallback**属性页回调到每个页面每个 PROPSHEETPAGE 结构的成员该页面的函数。

请参阅的详细信息的 Microsoft Windows SDK 文档：

-   创建属性页和结构、 函数和属性页的通知

-   对话框回调过程、 消息和结构

 

 





