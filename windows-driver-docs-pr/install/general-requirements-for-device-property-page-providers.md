---
title: 针对设备属性页提供程序的一般要求
description: 针对设备属性页提供程序的一般要求
ms.assetid: 91e93679-8c0c-43e7-a7d9-72bd0a464406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1d72eef250a6128c519ec3f4ea893dbe872307
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519387"
---
# <a name="general-requirements-for-device-property-page-providers"></a>针对设备属性页提供程序的一般要求


若要创建设备属性页，提供程序必须遵循这些常规要求按顺序的属性页后，可以正常工作：

-   处理请求，以便添加属性页。

    提供程序属性页面扩展 Dll，发出此请求通过**AddPropSheetPageProc**回调函数。 有关详细信息，请参阅[设备属性页提供程序 (属性页扩展 Dll) 的特定要求](specific-requirements-for-device-property-page-providers--property-pag.md)

-   通过调用创建的属性页**CreatePropertySheetPage**函数。 提供程序将此调用中传递初始化 PROPSHEETPAGE 结构的地址。

-   提供**PropSheetPageProc**处理 PSPCB_CREATE 和 PSPCB_RELEASE 的回调函数时必须分配额外的存储，并将其属性页发布消息。

-   提供处理 Windows 消息的每个自定义属性页对话框过程。
-   PROPSHEETPAGE 结构 （除其他事项外） 的地址初始化**PropSheetPageProc**回调函数和对话框框中的过程。

本部分包括以下主题提供有关自定义属性页的更多指导：

[创建自定义属性页](creating-custom-property-pages.md)

[属性页的回调函数](property-page-callback-function.md)

[处理 Windows 消息的属性页](handling-windows-messages-for-property-pages.md)

[示例自定义属性页](sample-custom-property-page.md)

 

 





