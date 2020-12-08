---
title: 手动添加设备元数据包
description: 手动添加设备元数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25677dd2e52f6cd1c0a1e4c5a3b68361bd7630b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790551"
---
# <a name="manually-adding-device-metadata-packages"></a>手动添加设备元数据包


可以通过以下方式在计算机上安装设备元数据包：

-   OEM 可以使用 Windows 7 OEM 预安装工具包 (OPK) 来更新操作系统的脱机映像。 OEM 使用 OPK 将设备元数据包复制到映像的 [设备元数据存储](device-metadata-store.md)。

-   开发人员可以将其设备元数据包复制到 [设备元数据存储区](device-metadata-store.md) ，以测试和调试包的安装。 有关详细信息，请参阅 [调试设备元数据包](debugging-device-metadata-packages-by-using-event-viewer.md)。

    **注意**  我们不建议最终用户将设备元数据包复制到设备元数据存储。 相反，最终用户应该使用 Windows 元数据和 Internet 服务 (WMIS) 或由 OEM 提供的安装应用程序来安装设备元数据包。

     

以下路径显示了 [设备元数据存储](device-metadata-store.md)的位置：

```cpp
%PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore
```

若要将设备元数据包复制到 [设备元数据存储](device-metadata-store.md)，请完成以下步骤：

1.  如果设备元数据包的区域设置的设备元数据存储中不存在子目录，则必须使用目标区域设置的名称创建该子目录。

    例如，如果包的区域设置为 EN-US，则必须首先创建以下目录（如果当前不存在）：

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataStore\EN-US
    ```

2.  将设备元数据包复制到 [设备元数据存储](device-metadata-store.md)的相应 *&lt; 区域设置 &gt;* 子目录。

设备元数据包安装到 [设备元数据存储](device-metadata-store.md)中后， [设备元数据检索客户端](device-metadata-retrieval-client.md) (DMRC) 访问设备元数据包，并向设备和打印机用户界面显示设备信息。

 

 





