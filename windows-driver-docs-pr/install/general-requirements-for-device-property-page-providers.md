---
title: 设备属性页提供程序的常规要求
description: 设备属性页提供程序的常规要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b89cb7ca671f4178cc03563dd49575fa8d252e5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820145"
---
# <a name="general-requirements-for-device-property-page-providers"></a>设备属性页提供程序的常规要求


若要创建设备属性页，提供程序必须遵循这些常规要求才能使属性页正常工作：

-   处理添加属性页的请求。

    对于作为属性页扩展 Dll 的提供程序，此请求通过 **AddPropSheetPageProc** 回调函数发出。 有关详细信息，请参阅 [设备属性页提供程序的特定要求 (属性页扩展 dll) ](specific-requirements-for-device-property-page-providers--property-pag.md)

-   通过调用 **CreatePropertySheetPage** 函数创建属性页。 提供程序在此调用中传递已初始化的 PROPSHEETPAGE 结构的地址。

-   提供一个 **PropSheetPageProc** 回调函数，该函数可处理 PSPCB_CREATE 和 PSPCB_RELEASE 消息（如果必须为属性页分配和释放附加的存储）。

-   为每个自定义属性页提供处理 Windows 消息的对话框过程。
-   在 **PropSheetPageProc** 回调函数和对话框过程的地址) ，使用 (初始化 PROPSHEETPAGE 结构。

本部分包括以下主题，这些主题提供有关自定义属性页的更多指导：

[创建自定义属性页](creating-custom-property-pages.md)

[属性页回调函数](property-page-callback-function.md)

[处理属性页的 Windows 消息](handling-windows-messages-for-property-pages.md)

[自定义属性页示例](sample-custom-property-page.md)

 

 





