---
title: 通过应用程序安装设备元数据包
description: 通过应用程序安装设备元数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbee7b3857aa78fec83ec730c67e38c4fb499455
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794871"
---
# <a name="installing-device-metadata-packages-through-an-application"></a>通过应用程序安装设备元数据包


若要使用应用程序（如设备安装应用程序）在 [设备元数据存储区](device-metadata-store.md) 中安装设备元数据包，请执行以下步骤：

1.  应用程序首先通过调用[SHGetKnownFolderPath](/windows/win32/api/shlobj_core/nf-shlobj_core-shgetknownfolderpath)函数来查询[设备元数据存储区](device-metadata-store.md)的路径。 设备元数据存储的 [KNOWNFOLDERID](/previous-versions//bb762584(v=vs.85)) GUID 为 {5CE4A5E9-E4EB-479D-B89F-130C02886155}。

2.  然后，应用程序通过调用 [CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596) 函数将设备元数据包复制到设备元数据存储区。

    **注意**  应用程序必须使用管理员权限运行，或者从提升的命令提示符窗口启动。



当应用程序将设备元数据包复制到 [设备元数据存储](device-metadata-store.md)时，必须完成以下步骤：

1.  如果设备元数据包的区域设置的设备元数据存储中不存在子目录，则该应用程序必须使用目标区域设置的名称创建该子目录。

    例如，如果包的区域设置为 EN-US，则当子目录当前不存在时，应用程序必须在设备元数据存储路径下创建 *en-us* 子目录。

2.  将设备元数据包复制到 [设备元数据存储](device-metadata-store.md)中的相应 *&lt; 区域设置 &gt;* 子目录。

    **注意** 如果使用 [CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)函数复制设备元数据包，请指定完整路径名称，其中包括相应的 *&lt; 区域设置 &gt;* 子目录。 通过执行此操作， [CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596) 将为包创建关联的子目录（如果它们不存在于本地计算机上）。




设备元数据包安装到 [设备元数据存储](device-metadata-store.md)中后， [设备元数据检索客户端](device-metadata-retrieval-client.md) (DMRC) 访问设备元数据包，并向设备和打印机用户界面显示设备信息。
