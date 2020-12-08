---
title: 用户界面扩展注册表项
description: 用户界面扩展注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3257bb7c0c7bd92cc54213b40428dd892f022744
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827101"
---
# <a name="user-interface-extension-registry-entries"></a>用户界面扩展注册表项





必须为每个扩展提供 COM 服务器类 ID。 请注意，每个扩展的 COM 服务器的类 ID 作为注册表项列出， (不是 CLSID \\ {WIA \_ DIP \_ ui clsid} shellex 下的值) \_ \\ ，其中，WIA \_ dip \_ ui \_ clsid 是应用程序请求此属性时返回的实际 GUID。 应用程序使用它作为注册表中的查找密钥的一部分。 每个扩展性接口都可以引用不同的类 ID。 不要求同一个对象全部实现它们。 仅列出已实现的扩展。 不需要列出所有四个。

由于类 ID GUID 标识要使用的驱动程序，如果设备的所有型号使用同一个驱动程序，则它们可以具有相同的类 ID GUID。 如果不同的模型使用不同的驱动程序，则它们必须具有不同的 Guid。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-contextmenuhandlers--clsid-of-com-in-process-server-"></a>CLSID \\ {WIA \_ DIP \_ UI \_ CLSID} \\ shellex \\ ContextMenuHandlers \\ &lt; COM 进程内服务器的 clsid&gt;  
供应商提供的用于实现上下文菜单 UI 扩展的 COM DLL。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-propertysheethandlers--clsid-of-com-in-process-server-"></a>CLSID \\ {WIA \_ DIP \_ UI \_ CLSID} \\ shellex \\ PropertySheetHandlers \\ &lt; COM 进程内服务器的 clsid&gt;  
供应商提供的用于实现属性表 UI 扩展的 COM DLL。

<a href="" id="clsid--wia-dip-ui-clsid--shellex-wiadialogextensionhandlers--clsid-of-com-in-process-server-"></a>CLSID \\ {WIA \_ DIP \_ UI \_ CLSID} \\ shellex \\ WiaDialogExtensionHandlers \\ &lt; COM 进程内服务器的 clsid&gt;  
供应商提供的用于实现应用程序对话框 UI 扩展的 COM DLL。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-default-value"></a>\\ &lt; COM 进程内服务器 &gt; \\ INPROCSERVER32 \\ 默认值的 clsid clsid  
\_包含供应商提供的用于实现扩展性接口的 COM 服务器的名称的 REG SZ 类型。

<a href="" id="clsid--clsid-of-the-com-in-process-server--inprocserver32-threadingmodel"></a>\\ &lt; COM 进程内服务器 &gt; \\ InProcServer32 ThreadingModel 的 clsid clsid \\  
\_包含供应商提供的 COM 服务器的线程模型名称的 REG SZ 类型。 将此项设置为单元。

 

 




