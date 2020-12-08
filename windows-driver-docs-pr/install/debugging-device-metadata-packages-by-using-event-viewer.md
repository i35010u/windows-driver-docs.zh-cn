---
title: 使用事件查看器调试设备元数据包
description: 使用事件查看器调试设备元数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 080b56e2139832f59a7bc2d00f013b57ed7e780f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782925"
---
# <a name="debugging-device-metadata-packages-by-using-event-viewer"></a>使用事件查看器调试设备元数据包


从 Windows 7 开始，Windows (ETW) 服务的事件跟踪支持与设备元数据包处理相关的事件的 DeviceMetadata/调试通道。

DeviceMetadata/调试通道存储在下载或处理设备元数据包期间发生的错误和信息性事件。 此通道还存储警告和信息性事件，这些事件提供有关检测和查询设备元数据 [存储](device-metadata-store.md)中的设备元数据包的附加状态。

### <a name="viewing-device-metadatadebug-etw-events-through-event-viewer"></a>通过事件查看器查看设备元数据/调试 ETW 事件

您可以使用事件查看器查看为设备元数据包记录的事件。 请按照以下步骤在事件查看器中打开 DeviceMetadata/Debug ETW 通道，查看这些事件：

1.  在 " **开始** " 菜单上，右键单击 " **计算机**"，然后单击 " **管理**"。

2.  展开 " **系统工具** " 节点。

3.  展开，然后单击 " **事件查看器** " 节点。

4.  在 " **视图** " 菜单上，单击 " **显示分析和调试日志**"。

5.  展开 " **应用程序和服务日志** " 节点。

6.  展开 " **Microsoft** " 节点。

7.  展开 " **Windows** " 节点。

8.  展开 " **UserPnP** " 节点。

9.  单击 " **DeviceMetadata"/"调试** " 节点。

    **注意**  必须先在 DeviceMetadata/Debug ETW 通道上启用日志记录才能接收和查看事件。 为此，请右键单击 " **DeviceMetadata"/"调试** " 节点，然后选择 " **属性**"。 然后单击 " **启用日志**"。

     

### <a name="device-metadatadebug-etw-events"></a>设备元数据/调试 ETW 事件

在下载或处理设备元数据包期间，操作系统会记录以下错误、警告和信息性事件：

<a href="" id="event-id--7900-error--device-metadata-package-error"></a>事件 ID：7900错误：设备元数据包错误  
检测到设备元数据包的组件之一出现错误。

此事件日志消息包含以下信息：

-   错误的说明，其中包括错误源的说明。 错误源为 [设备元数据存储](device-metadata-store.md) 或 [设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

-   应用程序特定的错误代码。 有关这些错误代码的详细信息，请参阅 [设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

<a href="" id="event-id--7901-information--device-metadata-package-downloaded-from-wmis-"></a>事件 ID：7901信息：从 WMIS 下载的设备元数据包。  
设备元数据包是从 [Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md) (WMIS) 的设备元数据 [检索客户](device-metadata-retrieval-client.md))  (端下载的，它从包中提取组件并将它们保存在 [设备元数据缓存](device-metadata-cache.md)中。

此事件日志消息包含以下信息：

-   事件的说明。

-   [设备元数据缓存](device-metadata-cache.md)中解压缩设备元数据包的位置。

-   设备元数据包的名称。

<a href="" id="event-id--7902-error--device-metadata-package-not-signed--"></a>事件 ID：7902错误：设备元数据包未签名。   
已安装的设备元数据包不是由 [Windows Quality Online Services (Winqual) ](../dashboard/winqual-submission-tool--winqualexe-.md)签名的。

**注意**  仅当从 WMIS 下载设备元数据包时，才会验证该签名。

 

此事件日志消息包含以下信息：

-   对错误的说明。

-   设备元数据包的名称。

-   应用程序特定的错误代码。 有关这些错误代码的详细信息，请参阅 [设备元数据错误代码](device-metadata-error-codes.md)。

-   Win32 错误代码。

<a href="" id="event-id--7950-information--new-device-metadata-package-discovered-in-the-local-metadata-store-"></a>事件 ID：7950信息：本地元数据存储中发现的新设备元数据包。  
DMRC 检测到安装在本地计算机上的新设备元数据包。

此事件日志消息包含以下信息：

-   事件的说明。

-   设备元数据包的源，即 [设备元数据存储区](device-metadata-store.md) 或 [设备元数据缓存](device-metadata-cache.md)。

-   设备元数据包的名称。

<a href="" id="event-id--7951-information--query-for-metadata-packages-in-progress-"></a>事件 ID：7951信息：正在查询元包。  
DMRC 查询特定设备的已安装设备元数据包。

此事件日志消息包含以下信息：

-   事件的说明。

-   设备查找密钥，如设备的硬件 ID 或型号 ID。 有关详细信息，请参阅 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) 和 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))。

    **注意**   当硬件 Id 列表作为参数传递时，仅记录最特定的硬件 ID。

     

<a href="" id="event-id--7952-warning--network-related-errors-"></a>事件 ID：7952警告：网络相关错误。  
DMRC 在下载从 WMIS 打包的设备元数据时遇到网络错误。

**注意**   网络不可用时，不会生成此警告。

 

此事件日志消息包含以下信息：

-   该错误的详细说明。

-   应用程序特定的错误代码。 有关这些错误代码的详细信息，请参阅 [设备元数据错误代码](device-metadata-error-codes.md)。

-   出现网络错误时的 HTTP 状态代码。

