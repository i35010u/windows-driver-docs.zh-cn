---
title: 服务元数据
description: 服务元数据
ms.assetid: daf5db05-cf39-4ff2-a2f1-0ffd718c638e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b779bff8cc0e66a374077dae21e552ebabf45a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563624"
---
# <a name="service-metadata"></a>服务元数据

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

可以创建和提交服务元数据包，以创建与 Windows 深度集成的体验。 当 Windows 检测到匹配的运算符的服务元数据包的移动宽带硬件时，它会自动下载服务元数据和指定的移动宽带应用程序。

服务元数据包含描述一种服务，包括以下信息：

-   服务提供程序名称

-   一个或多个服务类别

-   移动宽带特有的信息

-   移动宽带应用

-   移动宽带的配置文件

-   预配 XML 的受信任的证书

-   [DeviceNotificationHandler](devicenotificationhandler.md)元素

-   [PrivilegedApplications](privilegedapplications.md)元素

元数据中的信息用于自定义的 Windows 8、 Windows 8.1 和 Windows 10 用户体验方面，并提供与移动宽带应用程序，以前称为移动运营商应用程序集成。

服务元数据包包含.devicemetadata ms 文件中存储的多个 XML 文档。 每个文档指定服务的属性的各种的组件。 这些 XML 文档提供 Windows 连接管理器显示的自定义操作用户，以及网络配置信息。

有关服务元数据包中的 XML 文档的参考信息，请参阅[服务的元数据数据包架构参考](service-metadata-package-schema-reference.md)。

## <a name="span-idservmdconspanspan-idservmdconspanservice-metadata-contents"></a><span id="servmdcon"></span><span id="SERVMDCON"></span>服务元数据内容


以下摘要描述的一些最有趣的字段都包含和内部服务元数据包定义：

- **硬件 Id**  
  对于 GSM 网络，可以提交元数据包，描述要用来匹配在服务元数据包的 IMSI 或 ICCID 范围。 如果你是 MVNO，可以指定一个或多个范围的 IMSIs 或已从 m n O 租用的 SIM ICC Id。 对于 CDMA 网络，可以使用提供程序 ID (SID/NID) 或提供程序名称来提交包。 硬件 Id 对应于[HardwareID](hardwareid.md)服务元数据包架构中的元素。 有关如何规划硬件标识 (HWID) 范围 m n O 和 MVNO 方案的详细信息，请参阅[对于 Mvno 传送体验](delivering-experiences-for-mvnos.md)

- **服务编号**  
  移动宽带服务提供程序的唯一 ID。 此 GUID 还用于确定运算符使用预配帐户的元数据时。 如果更新设备元数据包，此 GUID 必须保持不变。 该服务数字对应于[ServiceNumber](servicenumber.md)服务元数据包架构中的元素。

- **运算符徽标**   
  Windows 连接管理器中显示网络条目旁边的自定义徽标。 （徽标时处于隐藏状态用户漫游网络上。）运算符徽标对应于[ServiceIconFile](serviceiconfile.md)服务元数据包架构中的元素。 有关徽标要求的详细信息，请参阅[服务图标要求](https://msdn.microsoft.com/library/windows/hardware/dn236416)。  
  > [!IMPORTANT]
  > 在 Windows 10 版本 1709年及更高版本，此字段已替换为通过 COSA 品牌。 品牌 COSA 中的字段上的说明[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。 如果你面向的 Windows 10，版本 1709 之前, 的 Windows 版本仍会创建元数据包在本部分中所述。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。 

- **移动宽带应用**  
  UWP 设备应用会自动下载并应用于计算机。 此应用程序可以提供键体验计划购买、 数据使用情况和帮助和支持，例如，可以突出显示的增值服务。

- **MB 采购配置文件**  
  购买用于建立购买订阅的连接受到限制的配置文件。

  如果您是有用于所有订阅服务器只有一个采购 APN GSM 操作员，可以使用服务元数据来设置的计算机。 如果你有多个购买 APNs，应使用帐户预配的元数据来设置相应的购买 APN。 或者，您可以不执行任何操作，并使用存储在要提供 APN 连接信息的 APN 数据库条目。

- **MB Internet 配置文件**  
  每个移动宽带订阅可以有一个用于连接到家庭网络运算符的默认配置文件。 Windows 连接管理器使用此配置文件进行自动连接到网络。

  如果您是有用于所有订阅服务器只有一个 Internet APN GSM 操作员，可以使用服务元数据来设置计算机。 如果有多个 Internet APNs，应使用预配的元数据的帐户设置适当的 internet APN。 或者，您可以不执行任何操作，并使用存储在要提供 APN 连接信息的 APN 数据库条目。

- **证书数据**  
  用于预配的证书信息。 这包括证书颁发者名称和使用者名称。 此信息用于确保启动的网站的帐户预配操作由受信任的操作员。

- **自定义的运算符名称**  
  移动宽带设备通常提供 Windows Windows 连接管理器中显示的运算符名称。 可以通过在元数据中指定自定义名称来覆盖此名称。 此名称将显示仅当用户在家庭网络且不在漫游网络。 显示漫游的网络名称基于从设备收到的信息。 这对应于[ServiceProvider](serviceprovider.md)服务包元数据架构中的元素。  
  > [!IMPORTANT]
  > 在 Windows 10 版本 1709年及更高版本，此字段已替换为通过 COSA 品牌。 品牌 COSA 中的字段上的说明[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。 如果你面向的 Windows 10，版本 1709 之前, 的 Windows 版本仍会创建元数据包在本部分中所述。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。 

- **设备通知处理程序**  
  一般情况下，应用必须由用户运行之前它可以向系统事件代理注册的工作项的至少一次。 但是，移动宽带应用程序可能需要接收重要事件之前用户可以运行该应用。 您可以指定[DeviceNotificationHandler](devicenotificationhandler.md)服务元数据，Windows 将使用注册某些关键事件中的元素。 有关短信通知的详细信息，请参阅[交付体验来 Mvno](delivering-experiences-for-mvnos.md)。

- **特权应用有权访问移动宽带的受限接口列表**  
  移动宽带 Api 和接口 （包括帐户预配和短信） 到移动宽带应用程序只是受限制和可用。 可以在服务元数据包中指定的特权的应用程序有权访问这些特权的 Api 列表[PrivilegedApplications](privilegedapplications.md)元素。 特权的应用可以调试或测试应用程序;它们不需要通过 Microsoft Store 进行分发。

## <a name="span-idservicemetadatapackagestructurespanspan-idservicemetadatapackagestructurespanspan-idservicemetadatapackagestructurespanservice-metadata-package-structure"></a><span id="Service_Metadata_Package_Structure"></span><span id="service_metadata_package_structure"></span><span id="SERVICE_METADATA_PACKAGE_STRUCTURE"></span>服务元数据包结构


存储在压缩的 cab 文件以及必须具有文件扩展名的组件的服务元数据包 **.devicemetadata ms**。 服务元数据包将使用此文件扩展名，因为它们使用相同的基础平台作为设备元数据包。 在创建之前 **.devicemetadata ms**文件，必须先创建元数据包的全局唯一标识符 (GUID)。 然后，必须使用以下命名约定创建.devicemetadata ms 文件时：**&lt;GUID&gt;.devicemetadata ms**。

**请注意**  虽然的 cab 文件的常用文件扩展名 **.cab**，服务元数据包文件的文件扩展名必须是 **.devicemetadata ms**。 这是为了强调这一事实，最终用户不能解压缩或修改这些包。

 

有两种类型的服务元数据包： 一个区域设置服务元数据包和多个区域设置服务元数据包。

### <a name="span-idsinglelocaleservicemetadatapackagespanspan-idsinglelocaleservicemetadatapackagespanspan-idsinglelocaleservicemetadatapackagespansingle-locale-service-metadata-package"></a><span id="Single_Locale_Service_Metadata_Package"></span><span id="single_locale_service_metadata_package"></span><span id="SINGLE_LOCALE_SERVICE_METADATA_PACKAGE"></span>单个区域设置服务元数据包

服务元数据包中的可本地化资源是在 Windows 连接管理器和显示在它旁边的服务图标中显示的运算符名称。 如果不需要本地化你的名称或更改您基于从 PC 的区域设置信息的图标，创建单一的区域设置服务元数据包。 无论用户使用其 PC 的哪些区域设置，它们将获取运算符名称和服务在单个区域设置的服务元数据包中定义的图标。

单个区域设置服务元数据包必须具有以下文件结构：

![单个区域设置服务的元数据包结构](images/mb-xmlref-singlelocalesmp.jpg)

单个区域设置元数据包的一些注意事项：

-   图标文件可以有任何文件名。 但是，必须命名为单独 XML 文档**PackageInfo.xml**， **ServiceInfo.xml**， **WindowsInfo.xml**，和**SoftwareInfo.xml**.

-   名称**MobileBroadbandInfo.xml**文件中定义**ServiceInfo.xml**。 应使用该文件本文档中列出的名称。

-   **.Devicemetadata ms**文件不能包含"{"或"}"在名称中。 对于每个元数据包文件的名称 GUID 必须是唯一的。 当创建新的或修改服务元数据包时，必须创建新的 GUID，即使所做的更改是很微小的。

-   Windows 可识别的文件扩展名为服务元数据包 **.devicemetadata ms**。

### <a name="span-idmultiplelocaleservicemetadatapackagestructurespanspan-idmultiplelocaleservicemetadatapackagestructurespanspan-idmultiplelocaleservicemetadatapackagestructurespanmultiple-locale-service-metadata-package-structure"></a><span id="Multiple_Locale_Service_Metadata_Package_Structure"></span><span id="multiple_locale_service_metadata_package_structure"></span><span id="MULTIPLE_LOCALE_SERVICE_METADATA_PACKAGE_STRUCTURE"></span>多个区域设置服务元数据包结构

服务元数据包在一个包中支持多个区域设置文件。 如果为你的服务支持多个区域设置，您可以将多个区域设置文件放在一个服务元数据程序包。

如果您希望以显示你的服务的本地化的名称在网络列表 Windows 连接管理器中或为您的网络会显示不同的徽标 Windows 连接管理器中，可以使用多个本地服务元数据包。 Windows 将显示本地化的网络名称和徽标基于系统首选语言，在 Windows 安装过程通常会对其进行配置。 即使当前用户的语言不同于系统首选语言，图标和网络名称始终会出现在系统首选语言。 如果服务元数据包不包含区域设置，将显示的语言中性说明从根服务元数据包。 对于大多数用户自己的语言将匹配系统首选语言。

多个区域设置服务元数据包必须具有以下文件结构：

![多区域设置服务的元数据包结构](images/mb-xmlref-multiplelocalesmp.jpg)

多个区域设置元数据包的一些注意事项：

-   在每个文件夹中创建的区域设置名称文件夹并将相关的文件的 XML 文件放在区域设置名称文件夹中。

-   您仍然必须具有的顶级 XML 文件和相关文件，例如图标文件，每个文件夹的顶层。 在服务元数据包不包含区域设置时，这提供回退机制。

-   请确保所有必需的文件和这些文件中的字段完全填充在您创建的每个区域设置特定文件夹内。 其中不包括每个文件夹的最高级别中的内容。 例如， [ServiceNumber](servicenumber.md)必须填写 ServiceInfo.xml 中的元素，并将其复制和创建每个特定于区域设置的文件夹中的顶级文件夹。 如果不这样做会导致错误。

-   SoftwareInformation XML 文档不支持多个区域设置，因为不能指定每个区域设置的不同 SoftwareInfo.xml 文件。

## <a name="span-idmsdsubspanspan-idmsdsubspanservice-metadata-submission-and-maintenance"></a><span id="msdsub"></span><span id="MSDSUB"></span>服务元数据提交和维护


有关如何将提交到 Windows 开发人员中心仪表板 – 硬件，服务元数据包的详细信息请参阅[用于创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

请务必保留包根据如何描述最新的 IMSI 和 ICCID 或 CDMA 提供程序名称或 SID 值匹配的元数据。 这可能需要的 MNO 或 MVNO，以实现新的工作流是 SIM 或设备获取跟踪的 Sim 和 MNO 或 MVNO 到这些 ICCIDs 或 IMSIs 所提供的新订单的一部分。

它是最佳做法，避免进行频繁服务元数据通过保留 ICCID 或 IMSI 范围 （或 CDMA SIM/提供程序名称） 对 m n O 和更改 MVNO 提前，因此，当新 SIMs （或 CDMA 的设备） 是采购，它们已实现你服务元数据包。

如果你需要更新你在 Windows 开发人员中心硬件仪表板注册的服务标识符，请参阅[服务标识符所有权更新](service-identifier-ownership-updates.md)。

元数据更新是以无提示方式应用基于内部 Windows 逻辑 （通常每隔 8 天） 时 Windows 查询 WMIS 是否有更新元数据更新。

应用程序应设计为处理与它所引用的直到最新的元数据应用到系统的元数据的以前的版本。

[设计用户体验的移动宽带应用](designing-the-user-experience-of-a-mobile-broadband-app.md)提供了有关如何设计用户指南体验扩展到地址常见错误情况，例如缺少或无法识别该设备时。

 

 





