---
title: 用户界面扩展插件注册表项
description: 用户界面扩展插件注册表项
ms.assetid: 1ddf12a1-50e9-4f6e-9394-5bb1afb67798
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc4c4acea8ef9c38149f4c2e93c51135ae29442b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527170"
---
# <a name="user-interface-extension-registry-entries"></a>用户界面扩展插件注册表项





必须为每个扩展来提供 COM 服务器类 ID。 请注意，作为 CLSID 下的注册表项 （而不是值） 列出的类 ID 的 COM 服务器的每个扩展\\{WIA\_DIP\_UI\_CLSID}\\shellex，其中 WIA\_DIP\_UI\_CLSID 是当应用程序请求此属性时，返回的实际 GUID。 应用程序使用它作为在注册表中查找项的一部分。 每个扩展性接口可以指不同的类 id。 没有相同的对象实现所有这些要求。 列出的实现的扩展。 它不需要列出所有四个。

类 ID GUID 标识哪些驱动程序使用，如果你的设备的所有模型都使用相同的驱动程序，因为它们都可以有相同的类 ID GUID。 如果不同的模型使用不同的驱动程序，则必须具有不同的 Guid。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-contextmenuhandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\ContextMenuHandlers\\&lt;CLSID 的 COM 进程内服务器&gt;  
供应商提供 COM DLL 实现上下文菜单 UI 扩展。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-propertysheethandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\PropertySheetHandlers\\&lt;CLSID 的 COM 进程内服务器&gt;  
供应商提供 COM DLL 实现属性页 UI 扩展。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-wiadialogextensionhandlers--clsid-of-com-in-process-server-"></a>CLSID\\{WIA\_DIP\_UI\_CLSID}\\shellex\\WiaDialogExtensionHandlers\\&lt;CLSID 的 COM 进程内服务器&gt;  
供应商提供 COM DLL 实现应用程序对话框 UI 扩展。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-default-value"></a>CLSID\\&lt;COM 进程内服务器的 CLSID&gt;\\InProcServer32\\默认值  
REG\_SZ 类型包含的供应商提供的 COM 服务器实现扩展性接口的名称。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-threadingmodel"></a>CLSID\\&lt;COM 进程内服务器的 CLSID&gt;\\InProcServer32\\ThreadingModel  
REG\_SZ 类型包含的供应商提供 COM 服务器的线程模型的名称。 将此项设置为单元。

 

 




