---
title: 服务元数据概述
description: 服务元数据概述
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: d26b5276cfe5fe2b560df831170e08b48bdaa407
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827025"
---
# <a name="service-metadata-overview"></a>服务元数据概述

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

你可以创建和提交服务元数据包，以创建与 Windows 深度集成的体验。 当 Windows 检测到与操作员的服务元数据包匹配的移动宽带硬件时，它会自动下载服务元数据和指定的移动宽带应用。

服务元数据包含描述服务的信息，包括以下内容：

- 服务提供商名称

- 一个或多个服务类别

- 移动宽带特定的信息

- 移动宽带应用

- 移动宽带配置文件

- 用于预配 XML 的可信证书

- [DeviceNotificationHandler](devicenotificationhandler.md) 元素

- [PrivilegedApplications](privilegedapplications.md) 元素

元数据中的信息用于自定义 Windows 8、Windows 8.1 和 Windows 10 用户体验的各个方面，并提供与移动宽带应用（以前称为移动运营商应用程序）的集成。

服务元数据包由 devicemetadata-ms 文件中存储的多个 XML 文档组成。 每个文档都指定了服务属性的各种组件。 这些 XML 文档向 Windows 连接管理器提供了向用户显示的自定义，以及网络配置信息。

有关服务元数据包中 XML 文档的参考信息，请参阅 [服务元数据包架构参考](mobilebroadbandinfo-xml-schema.md)。

## <a name="service-metadata-contents"></a>服务元数据内容

下面的摘要介绍了服务元数据包中包含并定义的一些最感兴趣的字段：

- **硬件 Id**  
  对于 GSM 网络，可以提交一个元数据包，用于描述你希望服务元数据包匹配的 IMSI 或 ICCID 范围。 如果你是 MVNO，则可以指定一个或多个从 o 租赁的 IMSIs 或 SIM ICC Id 范围。 对于 CDMA 网络，可以使用提供程序 ID (SID/NID) 或提供程序名称提交包。 硬件 Id 对应于服务元数据包架构中的 [HardwareID](hardwareid.md) 元素。 有关如何规划硬件标识的详细信息 (HWID) 范围用于 o 和 MVNO 方案，请参阅为 [Mvno 提供体验](delivering-experiences-for-mvnos.md)

- **服务编号**  
  移动宽带服务提供商的唯一 ID。 使用帐户预配元数据时，此 GUID 还用于标识操作员。 如果更新设备元数据包，则此 GUID 必须保持不变。 服务编号对应于服务元数据包架构中的 [ServiceNumber](servicenumber.md) 元素。

- **运算符徽标** 出现在网络条目旁边的 "Windows 连接管理器" 中的自定义徽标。  (在用户处于漫游网络上时隐藏徽标。 ) 操作员徽标对应于服务元数据包架构中的 [ServiceIconFile](serviceiconfile.md) 元素。 有关徽标要求的详细信息，请参阅 [服务图标要求](../dashboard/index.yml)。  
  > [!IMPORTANT]
  > 在 Windows 10 版本1709及更高版本中，此字段已通过 COSA 的品牌替换。 COSA for 署名中的字段在 [规划桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)中进行了介绍。 如果在 Windows 10 版本1709之前面向 Windows 版本，则仍将创建此部分中所述的元数据包。 有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。

- **移动宽带应用**  
  自动下载并应用于计算机的 UWP 设备应用。 此应用程序可提供重要的体验，例如规划购买、数据使用、帮助和支持，并可以突出显示增值服务。

- **MB 购买配置文件**  
  用于建立用于购买订阅的有限连接性的购买配置文件。

  如果你是一位 GSM 操作员，其中只有一个购买 APN 用于所有订阅者，则可以使用服务元数据将其预配到计算机。 如果有多个购买 APNs，则应使用帐户预配元数据来设置相应的购买 APN。 或者，你可以不执行任何操作，而使用存储在 APN 数据库中的条目来提供 APN 连接信息。

- **MB Internet 配置文件**  
  每个移动宽带订阅可以有一个用于连接到家庭网络操作员的默认配置文件。 Windows 连接管理器使用此配置文件自动连接到网络。

  如果你是一个 GSM 操作员，其中只有一个 Internet APN 用于所有订阅者，则可以使用服务元数据来设置计算机。 如果有多个 Internet APNs，则应使用帐户预配元数据来设置相应的 internet APN。 或者，你可以不执行任何操作，而使用存储在 APN 数据库中的条目来提供 APN 连接信息。

- **证书数据**  
  用于预配的证书信息。 这包括证书颁发者名称和使用者名称。 此信息用于确保由网站启动的帐户预配操作由受信任的操作员颁发。

- **自定义操作员名称**  
  移动宽带设备通常提供操作员名称，Windows 连接管理器中显示该名称。 可以通过在元数据中指定自定义名称来覆盖此名称。 仅当用户在家庭网络上且不在漫游网络上时，才显示此名称。 显示的漫游网络名称基于从设备接收的信息。 这对应于服务包元数据架构中的 [ServiceProvider](serviceprovider.md) 元素。  
  > [!IMPORTANT]
  > 在 Windows 10 版本1709及更高版本中，此字段已通过 COSA 的品牌替换。 COSA for 署名中的字段在 [规划桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)中进行了介绍。 如果在 Windows 10 版本1709之前面向 Windows 版本，则仍将创建此部分中所述的元数据包。 有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。 

- **设备通知处理程序**  
  通常，应用必须至少运行一次，然后才能将工作项注册到系统事件代理。 但是，移动宽带应用可能需要在用户可以运行应用之前接收重要事件。 你可以在服务元数据中指定 [DeviceNotificationHandler](devicenotificationhandler.md) 元素，Windows 将使用它来注册某些关键事件。 有关 SMS 通知的详细信息，请参阅 [提供 mvno 体验](delivering-experiences-for-mvnos.md)。

- **有权访问移动宽带限制接口的特权应用的列表**  
  移动宽带 Api 和接口 (包括帐户预配和 SMS) 受限且仅可用于移动宽带应用。 可在 [PrivilegedApplications](privilegedapplications.md) 元素的服务元数据包中指定具有这些特权 api 访问权限的特权应用的列表。 特权应用可以是调试或测试应用;不需要通过 Microsoft Store 来分发它们。

## <a name="span-idservice_metadata_package_structurespanspan-idservice_metadata_package_structurespanspan-idservice_metadata_package_structurespanservice-metadata-package-structure"></a><span id="Service_Metadata_Package_Structure"></span><span id="service_metadata_package_structure"></span><span id="SERVICE_METADATA_PACKAGE_STRUCTURE"></span>服务元数据包结构


服务元数据包的组件存储在压缩的 cab 文件中，并且其文件扩展名必须为 **devicemetadata-ms**。 服务元数据包使用此文件扩展名，因为它们使用与设备元数据包相同的基础平台。 在创建 **devicemetadata-ms** 文件之前，必须先为元数据包创建 (GUID) 的全局唯一标识符。 然后，在创建 devicemetadata-ms 文件时，必须使用以下命名约定： **&lt; &gt; devicemetadata-ms**。

**注意**  
尽管 cabinet 文件的常规文件扩展名为 **.cab**，但服务元数据包文件的文件扩展名必须是 **. devicemetadata-ms**。 这是为了使最终用户不能解压缩或修改这些包这一事实。

有两种类型的服务元数据包：单一区域设置服务元数据包和多区域设置服务元数据包。

### <a name="single-locale-service-metadata-package"></a>单个区域设置服务元数据包

服务元数据包中的可本地化资源是在 Windows 连接管理器中显示的操作员名称，以及显示在它旁边的 "服务" 图标。 如果不需要根据电脑中的区域设置信息本地化名称或更改图标，请创建单个区域设置服务元数据包。 无论用户在自己的 PC 上使用何种区域设置，他们都将获取在单个区域设置服务元数据包中定义的 "操作员名称" 和 "服务" 图标。

单个区域设置服务元数据包必须具有以下文件结构：

![单个区域设置服务元数据包结构](images/mb-xmlref-singlelocalesmp.jpg)

单个区域设置元数据包的一些注意事项：

- 图标文件可以有任何文件名。 但是，必须将各个 XML 文档命名为 **PackageInfo.xml**、 **ServiceInfo.xml**、 **WindowsInfo.xml** 和 **SoftwareInfo.xml**。

- **MobileBroadbandInfo.xml** 文件的名称是在 **ServiceInfo.xml** 中定义的。 应为该文件使用本文档中列出的名称。

- **Devicemetadata-ms** 文件不能在名称中包含 "{" 或 "}"。 每个元数据包文件名的 GUID 都必须是唯一的。 当你创建新的或已修改的服务元数据包时，你必须创建新的 GUID，即使这些更改很小。

- Windows 将识别文件扩展名为 **devicemetadata-ms** 的服务元数据包。

### <a name="multiple-locale-service-metadata-package-structure"></a>多区域设置服务元数据包结构

服务元数据包在一个包中支持多个区域设置文件。 如果为服务支持多个区域设置，则可以将多个区域设置文件放入一个服务元数据包。

如果要在 Windows 连接管理器网络列表中显示服务的本地化名称，或者在 Windows 连接管理器中显示网络的不同徽标，则可以使用多个本地服务元数据包。 Windows 将根据系统首选语言显示本地化网络名称和徽标，通常在 Windows 安装程序过程中配置此语言。 即使当前用户的语言与系统首选语言不同，该图标和网络名称始终会以系统首选语言显示。 如果服务元数据包不包含区域设置，则将显示服务元数据包的根目录中的非特定语言说明。 对于大多数用户，其语言将与系统首选语言匹配。

多区域设置服务元数据包必须具有以下文件结构：

![多区域设置服务元数据包结构](images/mb-xmlref-multiplelocalesmp.jpg)

多区域设置元数据包的一些注意事项：

- 在每个文件夹中创建区域设置名称文件夹，并将 XML 文件或相关文件放在区域设置名称文件夹中。

- 你仍必须在每个文件夹的顶层有顶级 XML 文件和相关文件，例如图标文件。 这会在服务元数据包中未包含区域设置时提供回退机制。

- 确保所有必需的文件和这些文件中的字段已完全填充到你创建的每个区域设置特定的文件夹中。 这是对每个文件夹顶层内容的补充。 例如，ServiceInfo.xml 中的 [ServiceNumber](servicenumber.md) 元素必须在顶级文件夹中以及创建的每个特定于区域设置的文件夹中进行填充和复制。 否则将导致错误。

- SoftwareInformation XML 文档不支持多个区域设置，因为不能为每个区域设置指定不同的 SoftwareInfo.xml 文件。

## <a name="service-metadata-submission-and-maintenance"></a>服务元数据提交和维护

有关如何向 Windows 开发人员中心仪表板（硬件）提交服务元数据包的详细信息，请参阅 [创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

重要的是，将元数据包保持为最新，以了解它们的描述方式以及它们匹配的 IMSI 和 ICCID 或 CDMA 提供程序名称或 SID 值。 这可能需要 o 或 MVNO 来实现一个新的工作流，该工作流是 SIM 或设备获取的一部分，用于跟踪新的 Sim 顺序，以及要向其提供 Iccid 或 IMSIs 的 o 或 MVNO。

最佳做法是，通过保留 o 和 MVNO 的 ICCID 或 IMSI 范围 (或 CDMA SIM/提供程序名称) ，避免对服务元数据进行频繁的更改，以便在购买新的 Sim (或 CDMA) 设备时，它们已在服务元数据包中考虑。

如果需要更新在 Windows 开发人员中心硬件仪表板上注册的服务标识符，请参阅 [服务标识符所有权更新](service-identifier-ownership-updates.md)。

在 Windows 查询 WMIS 是否有更新的元数据更新时，将基于内部 Windows (逻辑，以无提示方式应用元数据更新) 。

应用应设计为处理其引用的以前版本的元数据，直到将最新的元数据应用到系统。

[设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md) 提供了有关如何设计用户体验来解决常见错误情况（如设备丢失或无法识别）的指导。
