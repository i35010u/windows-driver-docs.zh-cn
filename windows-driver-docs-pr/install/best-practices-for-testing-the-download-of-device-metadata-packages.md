---
title: 下载设备元数据包的最佳实践
description: 测试设备元数据包的下载的最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4136414c2922719825033d9501ee442f94acd9e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783173"
---
# <a name="best-practices-for-testing-the-download-of-device-metadata-packages"></a>测试设备元数据包的下载的最佳做法


由于设备元数据检索客户端 ([DMRC](device-metadata-retrieval-client.md)) 缓存元数据包的方式，在 Windows 元数据和 Internet 服务 ([WMIS](windows-metadata-and-internet-services.md)) server 上提供设备元数据包的时间与 DMRC 下载元数据包到客户端系统的时间之间可能会出现延迟。 若要测试设备元数据包的下载，可以通过以下方式之一来强制下载：

-   删除 [设备元数据缓存](device-metadata-cache.md)中的文件夹。 此缓存位于以下目录中：

    Windows 7：

    ```cpp
    %LOCALAPPDATA%\Microsoft\Device Metadata\
    ```

    Windows 8：

    ```cpp
    %PROGRAMDATA%\Microsoft\Windows\DeviceMetadataCache\
    ```

    删除这些文件夹将重置 **LastCheckedDate** 的值，并强制 DMRC 为所有设备查询 WMIS 服务器。

-   将 **CheckBackMDRetrieved** 和 **CheckBackMDNotRetrieved** 注册表项设置为0。 如果这些值为零，则 DMRC 会立即查询目标设备的 WMIS 服务器。

    请注意，WMIS 服务器每次从 WMIS 收到响应时都会覆盖这些值。 因此，如果 DMRC 在为目标设备查询 WMIS 服务器之前接收到其他任何设备的响应，则这些参数可能会更改。

    **注意**  只有在测试元数据包时才必须进行这些更改。 你不能向最终用户提供任何工具来更改 DMRC 使用的注册表值。

     

 

 





