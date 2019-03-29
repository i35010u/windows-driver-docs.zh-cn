---
title: 添加通知对象的注册表值
description: 添加通知对象的注册表值
ms.assetid: 8872a9b9-b7c5-4c10-b5d4-4fe880fc436f
keywords:
- 添加注册表部分 WDK 网络、 通知对象注册表值
- 通知对象 WDK 网络、 注册表值
- 网络通知对象 WDK，注册表值
- 注册表 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc082fffc5a5d0724f6ad19729190bfe726b7909
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563537"
---
# <a name="adding-registry-values-for-a-notify-object"></a>添加通知对象的注册表值





一个**NetTrans**， **NetClient**，或**NetService**组件可以具有通知对象执行一个或多个以下操作：

-   显示用于该组件的用户界面

-   通知，以便该组件可以运用绑定过程的某些控制绑定事件的组件

-   有条件地安装或删除软件组件

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

有关详细信息通知对象，请参阅[通知网络组件的对象](notify-objects-for-network-components.md)。

**请注意**  **Net**组件 （适配器） 不支持通知的对象; 因此，这些组件应使用共同安装程序。

 

有关共同安装程序的详细信息，请参阅[编写共同安装程序](https://msdn.microsoft.com/library/windows/hardware/ff554011)。

某个组件是否具有通知对象，必须添加该组件的 INF 文件 (通过*添加注册表部分*) 到组件的以下值**Ndi**密钥：

<a href="" id="clsid"></a>**ClsID**  
REG\_SZ 值，该值指定通知对象的 GUID （全局唯一标识符）。 通过运行 uuidgen.exe 实用程序来获取此 GUID。 有关此实用工具的详细信息，请参阅 Microsoft Windows SDK。

<a href="" id="componentdll"></a>**ComponentDll**  
REG\_SZ 值，该值指定通知对象 DLL 的路径。 **ComponentDll**必须指定 DLL 的完整路径，如果 DLL 不是在 Windows 中\\System32 目录。

以下是一种*添加注册表部分*，它将**ClsID**并**ComponentDll**值到**Ndi**密钥：

```INF
[MS_Protocol.ndi.reg]
HKR, Ndi, ClsID, 0, "GUID"
HKR, Ndi, ComponentDll, 0, "notifyobject.dll"
```

*DDInstall*部分的组件的通知对象还必须包含**CopyFiles**指令引用*文件列表部分*复制通知指定的目标目录对象 DLL **DestinationDirs**部分。 有关详细信息**CopyFiles**指令并**DestinationDirs**部分中，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

 

 





