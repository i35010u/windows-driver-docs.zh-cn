---
title: 通过应用程序安装设备元数据包
description: 通过应用程序安装设备元数据包
ms.assetid: 3fec5938-b81b-4efe-8bcd-b2ef4b1c4b8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d522b4f759455843b774385cf6781a359880d70d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369460"
---
# <a name="installing-device-metadata-packages-through-an-application"></a>通过应用程序安装设备元数据包


若要安装中的设备元数据包[设备元数据存储区](device-metadata-store.md)通过使用应用程序，例如设备安装应用程序，请执行以下步骤：

1.  应用程序在第一次查询的路径[设备元数据存储区](device-metadata-store.md)通过调用[SHGetKnownFolderPath](https://go.microsoft.com/fwlink/p/?linkid=145428)函数。 [KNOWNFOLDERID](https://go.microsoft.com/fwlink/p/?linkid=145429)设备元数据存储区的 GUID 是 {5CE4A5E9-E4EB-479D-B89F-130C02886155}。

2.  然后，应用程序复制到设备的元数据存储设备元数据包通过调用[CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)函数。

    **请注意**应用程序必须使用管理员特权运行或已开始从提升的命令提示符窗口。



当你的应用程序将复制到的设备元数据包[设备元数据存储区](device-metadata-store.md)，则必须完成以下步骤：

1.  如果你的设备元数据包的区域设置的设备元数据存储区中不存在一个子目录，则该应用程序必须使用的目标区域设置名称创建子目录。

    例如，如果包的区域设置为 EN-US，应用程序必须创建*EN-US*如果子目录当前不存在时，设备元数据存储区的路径下的子目录。

2.  将设备元数据包复制到适当 *&lt;区域设置&gt;* 中的子目录[设备元数据存储区](device-metadata-store.md)。

    **请注意**如果您使用[CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)函数将复制的设备元数据包，请指定完整路径名称，其中包括相应 *&lt;区域设置&gt;* 子目录。 通过执行此操作，请[CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)如果它们不存在本地计算机上创建您的包相关联的子目录。




设备元数据包安装后在[设备元数据存储区](device-metadata-store.md)，则[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 访问设备元数据包，并呈现到的设备信息设备和打印机用户界面。










