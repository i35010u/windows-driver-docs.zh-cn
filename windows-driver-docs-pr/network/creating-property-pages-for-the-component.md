---
title: 创建组件的属性页
description: 创建组件的属性页
ms.assetid: f353844f-56f4-42cd-8f7d-2fa87f469d3c
keywords:
- 通知对象 WDK 网络，属性页
- 网络通知对象 WDK，属性页
- 属性页 WDK 网络
- 属性 WDK 网络
- 属性页回调函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b779d07192345c16bb81e4643fe73e1d9f3f10a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211783"
---
# <a name="creating-property-pages-for-the-component"></a>创建组件的属性页





通知对象在网络配置子系统调用 notify 对象的 [**INetCfgComponentPropertyUi：： MergePropPages**](/previous-versions/windows/hardware/network/ff547746(v=vs.85)) 方法之后创建自定义属性页。 使用 **MergePropPages** 方法，可以将自定义属性页合并到组件的属性表上的默认页集中。 **MergePropPages** 将返回可用于合并自定义页面的适当数量的默认页面。

为了创建自定义属性页， **MergePropPages** 调用 COM **COTASKMEMALLOC** 函数为 PROPSHEETPAGE 结构的句柄分配内存。 其中每个句柄都表示要创建的属性页。 如果 **CoTaskMemAlloc** 成功分配了句柄的内存，则 **MergePropPages** 将为每个属性页声明并填充 **PROPSHEETPAGE** 结构。 **MergePropPages**填充这些结构后，将为每个属性页调用 Win32 **CreatePropertySheetPage**函数。 在此调用中， **MergePropPages** 传递要创建的 PROPSHEETPAGE 结构的地址。

还应为 **MergePropPages** 创建的每个属性页实现一个对话框回调函数。 对话框回调函数处理操作系统发送到与该对话框函数关联的属性页的消息。 若要将属性页与对话框函数关联， **MergePropPages** 应将每个页面的每个 PROPSHEETPAGE 结构的 **pfnDlgProc** 成员指向该页的对话框函数。

对话框函数处理以下消息：

-   WM \_ INITDIALOG 消息，该消息将在操作系统显示其关联属性页之前立即发送到对话框函数。 对话框函数通常使用此消息来初始化属性页并执行影响属性页外观的任务。

-   \_在属性页中发生事件后发送给对话框函数的 WM 通知消息。 与此消息一起发送的其他信息标识发生了什么事件。 此事件信息包含在指向 NMHDR 结构的指针中。 NMHDR 可以包含的属性表的信息包括：
    -   PSN \_ APPLY 事件，指示用户在属性页上单击 "确定"、"关闭" 或 "应用"。 如果用户单击 "确定"、"关闭" 或 "应用"，则对话框函数可以调用 **PropSheet \_ 更改** 的宏，以通知属性表该页中的信息已更改。 在此调用中，对话框函数将句柄传递给属性表和页。 对话框函数可以调用 Win32 **GetParent** 函数，并将句柄传递给页面以检索属性表的句柄。

        在对话框函数通知属性表发生更改后，网络配置子系统将调用 [**INetCfgComponentPropertyUi：： ValidateProperties**](/previous-versions/windows/hardware/network/ff547755(v=vs.85)) 方法来检查所有更改的有效性。 如果所有更改均有效，则子系统将调用 notify 对象的 [**INetCfgComponentPropertyUi：： ApplyProperties**](/previous-versions/windows/hardware/network/ff547741(v=vs.85)) 方法以使所有更改生效。 在操作系统关闭该对话框之前，网络配置子系统将调用 **ApplyProperties** 。

        可以实现 **ApplyProperties** 方法以检索用户输入的信息，并将信息设置为通知对象的数据成员。

    -   PSN \_ RESET 事件，指示操作系统即将销毁属性页。 用户可以单击属性页上的 "取消" 以启动此操作。 如果用户单击 "取消"，则网络配置子系统将调用 [**INetCfgComponentPropertyUi：： CancelProperties**](/previous-versions/windows/hardware/network/ff547742(v=vs.85)) 方法以使所有更改被忽略。 在关闭该对话框之前，网络配置子系统将调用 **CancelProperties** 。
    -   PSN \_ KILLACTIVE 事件，指示属性页即将变为非活动状态。 当用户激活另一页或单击 "确定" 时发生此事件。

还可以为**MergePropPages**创建的每个属性页实现*属性页回调*函数。 属性页回调函数执行页的初始化和清理操作。 若要将属性页与属性页回调函数关联， **MergePropPages** 应将每个页面的每个 PROPSHEETPAGE 结构的 **pfnCallback** 成员指向该页的属性页回调函数。

有关详细信息，请参阅 Microsoft Windows SDK 文档：

-   创建属性页和属性页的结构、函数和通知

-   对话框回调过程、消息和结构

 

