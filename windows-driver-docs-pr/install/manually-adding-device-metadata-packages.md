---
title: 手动添加设备元数据包
description: 手动添加设备元数据包
ms.assetid: 1d0cee1f-8aa7-4fa9-b3c7-797cd09a07f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2556262ee39e07c50793870d8b12e526a7a7325
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378363"
---
# <a name="manually-adding-device-metadata-packages"></a>手动添加设备元数据包


按以下方式，可以在计算机上安装设备元数据包：

-   OEM 可以使用 Windows 7 OEM 预安装工具包 (OPK) 来更新脱机映像的操作系统。 通过使用 OPK，OEM 将设备元数据包复制到的映像[设备元数据存储区](device-metadata-store.md)。

-   开发人员可以将复制到其设备元数据包[设备元数据存储区](device-metadata-store.md)测试和调试包的安装。 有关详细信息，请参阅[调试设备元数据包](debugging-device-metadata-packages.md)。

    **请注意**  我们不建议该最终用户复制设备元数据包到设备的元数据存储区。 相反，最终用户应通过使用 Windows 元数据和 Internet 服务 (WMIS) 或由 OEM 提供的安装应用程序安装设备元数据包。

     

在以下路径显示的位置[设备元数据存储区](device-metadata-store.md):

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore
```

若要复制的设备元数据打包到[设备元数据存储区](device-metadata-store.md)，完成以下步骤：

1.  如果你的设备元数据包的区域设置的设备元数据存储区中不存在一个子目录，您必须使用的目标区域设置名称创建子目录。

    例如，如果包的区域设置为 EN-US，您必须首先创建以下目录如果当前不存在：

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-US
    ```

2.  将你的设备元数据包复制到适当*&lt;区域设置&gt;* 子目录[设备元数据存储区](device-metadata-store.md)。

设备元数据包安装后在[设备元数据存储区](device-metadata-store.md)，则[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 访问设备元数据包，并呈现到的设备信息设备和打印机用户界面。

 

 





