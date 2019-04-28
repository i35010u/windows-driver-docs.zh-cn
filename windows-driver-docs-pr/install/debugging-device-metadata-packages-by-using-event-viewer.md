---
title: 使用事件查看器调试设备元数据包
description: 使用事件查看器调试设备元数据包
ms.assetid: 168a9dd1-aab2-4497-a59d-b8fe52d8cde2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10a6ba2d48a0d191822a799c9bb33e8f2308af01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352074"
---
# <a name="debugging-device-metadata-packages-by-using-event-viewer"></a>使用事件查看器调试设备元数据包


从 Windows 7 开始，到的设备元数据包处理相关的事件的事件跟踪 Windows (ETW) 服务支持 DeviceMetadata/调试通道。

DeviceMetadata/调试通道存储错误以及在下载或的设备元数据包处理期间发生的信息性事件。 此通道还将提供有关检测和查询设备的其他状态的元数据中的包的警告和信息性事件存储[设备元数据存储区](device-metadata-store.md)。

### <a name="viewing-device-metadatadebug-etw-events-through-event-viewer"></a>通过事件查看器查看设备元数据/调试 ETW 事件

有关设备元数据包，以查看记录的事件使用事件查看器。 请按照下列步骤来查看这些事件的事件查看器中打开 DeviceMetadata/调试 ETW 通道：

1.  上**启动**菜单中，右键单击**计算机**，然后单击**管理**。

2.  展开**系统工具**节点。

3.  展开，然后单击**事件查看器**节点。

4.  上**视图**菜单上，单击**显示分析和调试日志**。

5.  展开**应用程序和服务日志**节点。

6.  展开**Microsoft**节点。

7.  展开**Windows**节点。

8.  展开**UserPnP**节点。

9.  单击**DeviceMetadata/调试**节点。

    **请注意**  必须首先启用上 DeviceMetadata/调试 ETW 通道可以接收和查看事件日志记录。 若要执行此操作，右键单击**DeviceMetadata/Debug**节点，然后选择**属性**。 然后，单击**启用日志**。

     

### <a name="device-metadatadebug-etw-events"></a>设备元数据/调试 ETW 事件

操作系统在下载或设备元数据包的处理过程中记录以下错误、 警告和信息性事件：

<a href="" id="event-id--7900-error--device-metadata-package-error"></a>事件 ID:7900 错误：设备元数据包错误  
使用设备元数据包的组件之一检测到错误。

此事件日志消息包含以下信息：

-   错误，其中包括说明错误的源的说明。 错误源是[设备元数据存储区](device-metadata-store.md)或[设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

-   特定于应用程序的错误代码。 有关这些错误代码的详细信息，请参阅[设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

<a href="" id="event-id--7901-information--device-metadata-package-downloaded-from-wmis-"></a>事件 ID:7901 信息：从 WMIS 下载设备元数据包。  
设备元数据包从下载[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)(WMIS) 通过[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC)，该组件从包中提取和将保存在[设备元数据缓存](device-metadata-cache.md)。

此事件日志消息包含以下信息：

-   事件的说明。

-   打开包装后的设备元数据包中的位置[设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

<a href="" id="event-id--7902-error--device-metadata-package-not-signed--"></a>事件 ID:7902 错误：未签名的设备元数据包。   
已安装的设备元数据包不由签名[Windows Quality Online Services (Winqual)](https://go.microsoft.com/fwlink/p/?linkid=62651)。

**请注意**  仅当从 WMIS 下载时验证设备元数据包的签名。

 

此事件日志消息包含以下信息：

-   错误的说明。

-   设备元数据包的名称。

-   特定于应用程序的错误代码。 有关这些错误代码的详细信息，请参阅[设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

<a href="" id="event-id--7950-information--new-device-metadata-package-discovered-in-the-local-metadata-store-"></a>事件 ID:7950 信息：在本地元数据存储区中发现新设备元数据包。  
Dmrc 如何检测到新设备元数据包安装在本地计算机。

此事件日志消息包含以下信息：

-   事件的说明。

-   设备元数据包，为源[设备元数据存储区](device-metadata-store.md)或[设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

<a href="" id="event-id--7951-information--query-for-metadata-packages-in-progress-"></a>事件 ID:7951 信息：查询正在进行中的元数据程序包。  
Dmrc 如何查询安装特定设备的设备元数据包。

此事件日志消息包含以下信息：

-   事件的说明。

-   设备查找密钥，如设备的硬件 ID 或模型 id。 有关详细信息，请参阅[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)并[ **ModelID**](https://msdn.microsoft.com/library/windows/hardware/ff549295)。

    **请注意**  硬件的列表 Id 作为参数传递时，仅限最具体的硬件 ID 将记录。

     

<a href="" id="event-id--7952-warning--network-related-errors-"></a>事件 ID:7952 警告：与网络相关的错误。  
Dmrc 如何从 WMIS 打包的设备元数据下载期间遇到网络错误。

**请注意**  网络不可用时，不会生成此警告。

 

此事件日志消息包含以下信息：

-   错误的详细的说明。

-   特定于应用程序的错误代码。 有关这些错误代码的详细信息，请参阅[设备元数据错误代码](device-metadata-error-codes.md)。

-   网络错误时的 HTTP 状态代码。

 

 





