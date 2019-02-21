---
title: 用于测试的设备元数据包的下载的最佳实践
description: 用于测试的设备元数据包下载的最佳实践
ms.assetid: 4470fa63-527a-4e92-916f-a84421259f57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ee2209dbfca24f119e5d566d7f084b2beccb1da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546686"
---
# <a name="best-practices-for-testing-the-download-of-device-metadata-packages"></a>用于测试的设备元数据包下载的最佳实践


由于如何设备元数据检索客户端 ([dmrc 如何](device-metadata-retrieval-client.md)) 上 Windows 元数据提供设备元数据包的时间和 Internet 服务之间可以进行缓存元数据包，延迟 ([WMIS](windows-metadata-and-internet-services.md)) 服务器以及 dmrc 如何当下载到客户端系统的元数据包的时间。 若要测试的设备元数据包的下载，您可以通过以下方式之一强制下载：

-   删除文件夹中的[设备元数据缓存](device-metadata-cache.md)。 此缓存位于以下目录中：

    Windows 7:

    ```cpp
    %LOCALAPPDATA%\Microsoft\Device Metadata\
    ```

    Windows 8:

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
    ```

    删除这些文件夹的值重置**LastCheckedDate**并强制 dmrc 如何查询 WMIS 服务器的所有设备。

-   设置**CheckBackMDRetrieved**并**CheckBackMDNotRetrieved**为 0 的注册表项。 这些值都为零，dmrc 如何立即查询 WMIS 服务器为目标设备。

    请注意 WMIS 服务器覆盖这些值每次都 dmrc 如何接收来自 WMIS 的响应。 因此，如果 dmrc 如何接收响应的任何其他设备查询你的目标设备的 WMIS 服务器之前，可以更改这些参数。

    **请注意**  仅在测试元数据的包时，必须进行这些更改。 不，你必须向最终用户提供更改注册表值 dmrc 如何使用任何工具。

     

 

 





