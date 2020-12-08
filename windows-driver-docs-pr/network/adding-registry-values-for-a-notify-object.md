---
title: 添加通知对象的注册表值
description: 添加通知对象的注册表值
keywords:
- 添加-注册表--WDK 网络，通知对象注册表值
- 通知对象 WDK 网络，注册表值
- 网络通知对象 WDK，注册表值
- 注册表 WDK 通知对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53f28680c7a16d61750d4cd2519e88ab12ba36ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829995"
---
# <a name="adding-registry-values-for-a-notify-object"></a>添加通知对象的注册表值





**NetTrans**、 **NetClient** 或 **空间** 组件可以有一个执行下列一项或多项操作的 notify 对象：

-   显示组件的用户界面

-   通知绑定事件的组件，以便组件可以对绑定过程执行一些控制

-   有条件地安装或删除软件组件

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

有关通知对象的详细信息，请参阅 [为网络组件通知对象](notify-objects-for-network-components.md)。

**请注意**， (适配器的 **网络** 组件) 不支持通知对象;因此，这些组件应使用共同安装程序。  

 

有关共同安装程序的详细信息，请参阅 [编写共同安装程序](../install/writing-a-co-installer.md)。

如果某个组件包含 notify 对象，则该组件的 INF 文件必须通过 " *添加注册表" 部分* 添加 (，) 以下值添加到该组件的 **Ndi** 键：

<a href="" id="clsid"></a>**ClsID**  
一个 REG \_ SZ 值，该值指定通知对象的 GUID (全局唯一标识符) 。 通过运行 uuidgen.exe 实用程序来获取此 GUID。 有关此实用工具的详细信息，请参阅 Microsoft Windows SDK。

<a href="" id="componentdll"></a>**ComponentDll**  
一个 REG \_ SZ 值，该值指定通知对象 DLL 的路径。 如果 DLL 不在 Windows System32 目录中，则 **ComponentDll** 必须指定 dll 的完整路径 \\ 。

下面是将 **ClsID** 和 **ComponentDll** 值添加到 **Ndi** 项的 "*添加注册表" 部分* 的示例：

```INF
[MS_Protocol.ndi.reg]
HKR, Ndi, ClsID, 0, "GUID"
HKR, Ndi, ComponentDll, 0, "notifyobject.dll"
```

具有 "通知" 对象的组件的 *DDInstall* 部分还必须包含一个 **CopyFiles** 指令，该指令引用将通知对象 DLL 复制到 **DestinationDirs** 节指定的目标目录的 *文件列表部分*。 有关 **CopyFiles** 指令和 **DestinationDirs** 部分的详细信息，请参阅 [INF 文件部分和指令](../install/index.md)。

 

