---
title: 适用于 MVNO 的传送体验
description: 适用于 MVNO 的传送体验
ms.assetid: fcb2a3d4-bc19-4fa5-b81d-b0df287404a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b7ec3afffe4dc0e4e1ce07d8b90ae945a333558
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304260"
---
# <a name="delivering-experiences-for-mvnos"></a>适用于 MVNO 的传送体验

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

本主题提供有关如何将服务元数据与移动网络操作员 (o) 或移动虚拟网络运营商 (MVNO) 匹配的信息，以便在插入移动宽带设备时自动下载移动宽带应用。

为了成功匹配服务元数据，Windows 从插入到计算机中的 SIM 卡读取信息。 对于 CDMA 网络，会读取移动宽带设备本身。 然后，windows 将查询 Windows 元数据和 Internet 服务 (WMIS) 数据库下载正确的服务元数据包。 下载服务元数据包后，Windows 会将关联的移动宽带应用下载到计算机。

使用以下列表中适用于你的网络的链接：

-   [GSM 网络上的匹配](#matching-on-gsm-networks)

-   [CDMA 网络上的匹配](#matching-on-cdma-networks)

有关将服务元数据正确地匹配到 o 和 MVNO 所需的硬件的信息，请参阅 [移动运营商硬件概述](mobile-operator-hardware-overview.md)。

有关服务元数据的信息，请参阅 [服务元数据](service-metadata.md)。

有关服务元数据包架构的信息，请参阅 [服务元数据包架构参考](mobilebroadbandinfo-xml-schema.md)。

## <a name="matching-on-gsm-networks"></a>GSM 网络上的匹配


对于 GSM 网络 (3GPP) ，Windows 从 SIM 卡读取集成卡标识符 (ICCID) 和国际 Mobile 订户标识 (IMSI) 号。 必须从设备设置和检索这些号码。 如果 SIM 锁定并隐藏 IMSI 信息，则在解锁 SIM 卡之前，Windows 不会执行任何操作。 Windows 还从 SIM 或移动宽带设备读取 Home 提供程序名称。

如果设备中提供了 ICCID、IMSI 和 Home 提供程序名称，则 ICCID 和 IMSI 将去除最后两位数字，使用哈希算法进行编码，并以硬件 Id 形式发送到 WMIS (Hwid) ，以匹配服务元数据包。 已选中 Home 提供程序名称。 如果没有匹配项，则选中 ICCID。 如果没有匹配项，则选中 IMSI。 如果未找到匹配项，则不会下载任何服务元数据包。 Windows 大约每隔8天检查一次，以查看用户的移动宽带 SIM 是否有新的元数据。

### <a name="span-idmanaging_mvnosspanspan-idmanaging_mvnosspanspan-idmanaging_mvnosspanmanaging-mvnos"></a><span id="Managing_MVNOs"></span><span id="managing_mvnos"></span><span id="MANAGING_MVNOS"></span>管理 Mvno

如果你是一家为所有客户提供单一品牌的 o，则可以创建一个元数据包，其中包含了 MCC + MNC 的所有 IMSI 范围。 例如，如果您的 MCC + MNC 是 123 456，则可以创建一个涵盖123456000000000–123456999999999的元数据包。 这意味着，任何插入该范围内 SIM 的用户都将与你的体验相匹配。

如果一个或多个 Mvno 共享同一 MCC + MNC 值，则可能会变得更复杂。 下面介绍了一些处理此情况的策略。

**选项1：分段 IMSI 范围**

使用此选项时，o 不会在服务元数据包中定义 ICCID 范围，而是将定义 o 体验和 MVNO 体验的 IMSI 范围分段。 当匹配请求来自客户端设备时，它们的 IMSI 值将用于匹配该 SIM 的正确体验。

此方法要求 o 确保将 IMSI 范围保持为最新状态，并将 Mvno 分配到在可预测的 IMSI 数字块中的未来范围。

如果 ICCID 和 IMSI 均不与客户端计算机的请求匹配，则不匹配。

**注意**   IMSI 范围必须具有100粒度。 起始范围值必须以00结束，并且结束范围值必须以99结束。

 

*图1在 o 的 MCC +) MNC 中划分 IMSI 范围 (* ，其中显示了从 WMIS 请求服务元数据的客户端设备的示例，以及来自客户端的每个匹配请求是如何与体验匹配的。

![分段 imsi 范围](images/hck-winb-fig1-segmenting-imsi-ranges-matchingservicemetadata.jpg)

**图1在 o 的 MCC + MNC) 划分 IMSI 范围 (**

-   计算机 \# 1 的匹配请求与 o 定义的 IMSI 范围内的任何 ICCID 值不匹配。 O 服务元数据将下载到该计算机。

-   计算机 \# 2 的匹配请求与任何 ICCID 值或任何 IMSI 值都不匹配。 不会下载任何体验。

-   计算机 \# 3 的匹配请求与 MVNO A 的 IMSI 范围内的任何 ICCID 值不匹配。MVNO 服务元数据将下载到该计算机。

**选项2：分段 ICCID 范围**

使用此选项时，o 不会在服务元数据包中定义 IMSI 范围，而是将定义 o 体验和 MVNO 体验的 ICCID 范围分段。 当匹配请求来自客户端计算机时，ICCID 值将用于匹配该 SIM 的正确体验。

此方法要求 o 确保范围保持最新状态，并将 Mvno 分配到在可预测的 ICCID 数块中的未来范围。 如果在 SIM 制造过程中将大块的 Iccid 分配给 Sim，这可能是 o 及其 Mvno 的理想匹配策略。

如果 ICCID 与 IMSI 都不匹配来自客户端计算机的请求，则不匹配。

**注意**   IMSI 范围必须具有100粒度。 起始范围值必须以00结束，并且结束范围值必须以99结束。

 

*图2分段 ICCID 范围 (在 o 的 ICCID 颁发者标识号内) * 显示了从 WMIS 请求服务元数据的客户端计算机的示例，以及如何将来自客户端的每个匹配请求与体验相匹配。

![分段 iccid 范围](images/hck-winb-fig2-segmenting-iccid-ranges-matchingservicemetadata.jpg)

**图2在 o 的 ICCID 颁发者标识号 (划分 ICCID 范围) **

-   中的计算机 \# 1 的匹配请求包含在由 o 定义的 ICCID 范围内。 O 服务元数据将下载到该计算机。

-   计算机 \# 2 的匹配请求与任何 ICCID 值或任何 IMSI 值都不匹配。 不会下载任何体验。

-   计算机 \# 3 的匹配请求落在为 MVNO 定义的 ICCID 范围内。MVNO 服务元数据将下载到该计算机。

**选项3：使用 ICCID 范围和 o 以及 IMSI 范围描述 Mvno**

可以向 o 的整个基于 IMSI 的范围分配 (也就是说，其 "MCC + MNC" 值下的所有内容都) 。 然后，可以为任何 Mvno 分配其 Sim 的特定 ICCID 范围。 这意味着，除非该 SIM 存在 ICCID 匹配项，否则 SIM 会获得 o 体验。

此选项需要 o 或 MVNO，以确保将 ICCID 范围保持为最新状态，并将该 Mvno 分配到可预测 ICCID 数块的未来范围。 如果在 SIM 制造过程中将大块的 Iccid 分配给 Sim，这可能是 o 及其 Mvno 的理想匹配策略。 这意味着 o 的维护更少，因为其包跨越所有基于 IMSI 的范围。 在这种情况下，确保 MVNO 保持其 ICCID 范围保持最新状态非常重要;否则，MVNO 的客户可以与 o 体验相匹配。

**注意**   IMSI 范围必须具有100粒度。 起始范围值必须以00结束，并且结束范围值必须以99结束。

 

*图3使用 ICCID 定义 mvno，为 o 提供一个包含全部的 IMSI 范围* 的示例，该示例显示了从 WMIS 请求服务元数据的客户端计算机的示例，以及如何将来自客户端的每个匹配请求匹配到体验。

![使用 iccid 定义 mvno](images/hck-winb-fig3-using-iccid-to-define-mvnos-matchingservicemetadata.jpg)

*图3使用 ICCID 定义 Mvno 和 o 的全部 IMSI 范围*

-   计算机 \# 1 的匹配请求与 o 定义的 IMSI 范围内的任何 ICCID 值不匹配。 在该计算机上下载 o 服务元数据。

-   \#MVNO b 的 ICCID 范围中包含的计算机2的匹配请求将下载到该计算机。

-   计算机 \# 3 的匹配请求包含在 MVNO 的 ICCID 范围中。 MVNO a 的服务元数据将下载到该计算机。

-   计算机 \# 4 的匹配请求与 o 定义的 IMSI 范围内的任何 ICCID 值不匹配。 在该计算机上下载 o 服务元数据。

**选项4：对 ICCID 和 IMSI 范围进行分段**

可以混合使用 ICCID 范围和 IMSI 范围来描述 o 和 MVNO 网络。

**注意**   ICCID 范围获取第一个匹配的优先级。

 

这是最复杂的匹配模型。 若要确保正确匹配，o 和 MVNO 必须经常更新其服务元数据包。

*图4分段 ICCID 和 IMSI 范围* 显示了从 WMIS 请求服务元数据的客户端设备的示例，以及如何将来自客户端的每个匹配请求与体验进行匹配。

![分段 ccid 和 imsi 范围](images/hck-winb-fig4-segmenting-ccid-and-imsi-ranges-matchingservicemetadata.jpg)

*图4分段 ICCID 和 IMSI 范围*

-   计算机 \# 1 的匹配请求与任何 ICCID 值都不匹配，但包含在 o 定义的 IMSI 范围中。 O 服务元数据将下载到该计算机。

-   计算机 \# 2 的匹配请求包含在 MVNO b 的 ICCID 范围中。 MVNO b 的服务元数据将下载到该计算机。

-   计算机 \# 3 的匹配请求包含在 MVNO 的 ICCID 范围中。 MVNO a 的服务元数据将下载到该计算机。

-   计算机 \# 4 的匹配请求与任何 ICCID 值都不匹配，但包含在 o 定义的 IMSI 范围中。 O 服务元数据将下载到该计算机。

-   计算机 \# 5 的匹配请求与任何 ICCID 值都不匹配，但包含在 MVNO c 所定义的 IMSI 范围中。 MVNO C 的服务元数据将下载到该计算机。

**选项5：使用 GSM 网络的 Home 提供程序名称识别 o 和 MVNO**

使用此选项时，o 不会在服务元数据包中定义 IMSI 或 ICCID 范围，而是将定义 o 体验和 MVNO 体验的主提供程序名称分成一组。

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 设备报告一个提供程序名称值，该值唯一地标识 MVNO。 O 应具有其自己的提供程序名称值，以唯一标识它。

当匹配请求来自客户端计算机时，将使用 Home 提供程序名称来匹配该 SIM 的正确体验。

仅当不能使用 IMSI 和 ICCID 时，才建议使用此选项。

如果 Home 提供程序名称与来自客户端计算机的请求不匹配，则不匹配。

**注意**   家庭提供商名称必须是全局唯一的，以确保用户获得正确的体验。 服务元数据将只允许使用给定的主提供程序名称的单个服务元数据包。

 

*图5： GSM 网络的基于提供程序名称的匹配* 示例显示了从 Windows 元数据和 Internet 服务请求服务元数据 (WMIS) 服务的设备的示例，以及如何将设备的每个匹配请求与体验相匹配。

![使用 gsm 网络的家庭提供商名称](images/hck-winb-fig5-using-home-provider-name-for-gsm-networks-to-identify-the-mno-and-mvno.jpg)

*图 5 GSM 网络的基于提供程序名称的匹配*

-   计算机 \# 1 的匹配请求与 o 的主提供程序名称匹配。 下载 o 服务元数据。

-   计算机 \# 2 的匹配请求与任何提供程序名称值都不匹配。 不会下载任何体验。

-   计算机 \# 3 的匹配请求匹配 MVNO 的主提供程序名称。 MVNO a 的服务元数据已下载。

-   计算机 \# 4 的匹配请求与 MVNO b 的主提供程序名称匹配。将下载 MVNO b 的服务元数据。

**选项6：使用 Home Provider Name 和 o 以及 IMSI 范围描述 Mvno**

可以向 o 的整个基于 IMSI 的范围分配 (也就是说，其 "MCC + MNC" 值下的所有内容都) 。 然后，可以为任何 Mvno 分配特定的主提供程序名称。 这意味着，除非该设备的主提供商名称匹配，否则设备将获得 o 体验。

此选项需要 o 或 MVNO，以确保从设备报告的主提供商名称不会更改，全局唯一，并保持最新状态。 仅当不能使用 IMSI 和 ICCID 时，才建议使用此选项。

*图6使用 Home Provider Name 来定义 mvno，并为 o 显示了一个 IMSI 范围* ，其中显示了从 WMIS 请求服务元数据的客户端计算机的示例，以及来自客户端的每个匹配请求是如何与体验匹配的。

![使用 home 提供程序名称定义 mvno](images/hck-winb-fig6-using-home-provider-name-to-define-mvnos-and-an-all-encompassing-imsi-range-for-the-mno.jpg)

*图6使用 Home Provider Name 来定义 o 的 Mvno 和 IMSI 范围*

-   计算机 \# 1 的匹配请求与 MVNO A 的 Home 提供程序名称匹配。在该计算机上下载服务元数据的 MVNO。

-   计算机 \# 2 的匹配请求与任何 Home 提供程序名称值和在 o 定义的 IMSI 范围内不匹配。 在该计算机上下载 o 服务元数据。

-   计算机 \# 3 的匹配请求与 MVNO b 的主提供程序名称匹配。 MVNO b 的服务元数据将下载到该计算机。

-   计算机 \# 4 的匹配请求与任何 Home 提供程序名称值和在 o 定义的 IMSI 范围内不匹配。 在该计算机上下载 o 服务元数据。

**选项7：备用匹配方法**

如果这些方法都不能用于 o 的网络 (例如，o 无法跟踪 o 的客户和 MVNO 客户) 之间的 IMSI 和 ICCID 范围，以下是可用的替代方法。 这种方法不太适合上述任何选项，而是提供适用于 Windows 8、Windows 8.1 或网络上 Windows 10 客户的移动宽带解决方案。

**服务元数据**

此方法创建涵盖整个 o 网络的服务元数据包。 这通常是通过提交包含 o 网络上所有 MCC + MNC 值的 IMSI 范围来完成的，无 ICCID 范围。 不介绍 MVNO 范围。 服务元数据包具有通用品牌和在 Windows 连接管理器中显示的通用网络名称。 然后，服务元数据将引用在检测到 o 的 SIM 时自动从 Microsoft Store 下载的通用应用。

**确定网络隶属关系**

如果用户还没有计划，则当用户尝试使用 Windows 连接管理器连接到网络时，将打开该应用程序。

当应用程序运行时，它将执行以下操作之一：

-   提示用户在显示的 Mvno 和 o 网络的列表中标识其计划的网络。

-   使用 web 服务将有关用户的 SIM 的信息发送回 o 后端，以便操作员可以使用自定义逻辑来确定正确的用户网络品牌。

**自定义 Windows 连接管理器品牌**

确定用户的移动宽带数据计划从属关系后，移动宽带应用可以更改在 Windows 连接管理器中显示的徽标和网络名称。 这是通过使用帐户预配元数据实现的，操作员应用可通过它将基于 XML 的信息发送到与特定订阅者的计划信息相关的 Windows。

有关帐户预配的详细信息，请参阅 [帐户预配](account-provisioning.md)。

**服务元数据更新**

未来的服务元数据更新 (例如，提交到通用服务元数据包) 的任何更改都可以覆盖订户计算机上应用的署名。 为避免出现这种情况，我们建议，如有可能，请不要更新服务元数据包。 由于元数据包包含通用品牌，并涵盖了 o 的整个 IMSI 范围，因此对于此方案，不需要经常更新包。

如果必须更新服务元数据包，请确保移动宽带应用可以启动其他基于操作员提供的后端逻辑的帐户预配元数据操作。 通过这种方式，您可以指定在后端更新服务元数据的时间，并让应用程序定期检查后端，并根据需要应用帐户设置元数据信息。

**注意**   由于未对服务元数据进行版本控制，因此应用程序无法查询元数据的本地副本，以确定是否已通过使用帐户预配元数据进行的自定义更新或应用。 应用程序无法唤醒和响应应用于计算机的服务元数据更新。

通过 Windows 开发人员中心硬件仪表板和计算机接收更新的元数据的时间之间可能会出现延迟。

 

**在移动宽带应用中署名**

本主题中所述的前面步骤使你可以为 o/MVNO 的网络 rebrand Windows 连接管理器图标和网络名称。 不过，应用本身也可以更名。

可以在应用中 rebrand 以下各项：

-   应用内容本身 (也就是说，可针对特定操作员) 更改应用中的所有内容。 这是应用对其进行完全控制的代码。 根据 o/MVNO，可能需要更改应用内的帮助内容、导航选项、页面布局、颜色和品牌。

-   可以动态更新应用磁贴，以显示特定于操作员的特定映像和布局。 有关如何动态更新磁贴内容的信息，请参阅 [快速入门：发送磁贴更新](/previous-versions/windows/apps/hh465439(v=win.10))。

不能在应用中 rebrand 以下各项：

-   应用的名称。 你可以通过更改磁贴模板尝试隐藏名称，但无法更改名称本身或表示该应用的图标，因为它是在应用程序清单中定义的。

-   "设置" 超级按钮中的应用名称、信息和图标。

-   应用说明。

### <a name="span-idsim_reprogrammingspanspan-idsim_reprogrammingspanspan-idsim_reprogrammingspansim-reprogramming"></a><span id="SIM_reprogramming"></span><span id="sim_reprogramming"></span><span id="SIM_REPROGRAMMING"></span>SIM reprogramming

如果要动态重新编程 Sim 以更改 IMSI 或 ICCID，应注意 Windows 8、Windows 8.1 和 Windows 10 解释 reprogramming 的以下方式：

-   Reprogramming 要求设备的 IMSI 和 ICCID 缓存失效。 有多种方法可以完成此操作，具体取决于操作员网络和设备。

-   Reprogrammed SIM 后，设备会重新读取 SIM 信息。 它可以使用热 SIM 交换插入序列，让 Windows 知道它应重新查询新的 IMSI 和 ICCID 值。

-   必须更改 ICCID，否则 Windows 不会将 SIM 视为新 SIM。

-   如果仅更改了 IMSI，则 Windows 不会将 SIM 视为新的 SIM，并且不会下载服务元数据。 如果已为此 SIM 下载了不同的应用，则不会下载移动宽带应用。

若要获取新的服务元数据 (这会导致新的品牌) ，若要获取新的移动宽带应用以下载 ICCID 和 IMSI，则必须使用运算符的 reprogramming 方法更改服务数据和移动宽带应用。

## <a name="matching-on-cdma-networks"></a>CDMA 网络上的匹配


对于 CDMA 网络 (3GPP2) ，Windows 会将设备报告的 SID 和提供程序名称值读取到 WMIS 中的相应服务元数据包。 如果未找到匹配项，则不会下载任何服务元数据包。 Windows 大约每隔8天检查一次，查看是否存在新的设备元数据。 如果存在 SID 的服务元数据，并且提供程序名称存在单独的服务元数据包，并且这两个值都与设备所报告的 SID 和提供程序名称值匹配，则将匹配首选项提供给 SID。 在这种情况下，提供程序名称包不匹配。

**重要提示**   提供程序名称值区分大小写，并且必须与设备向 Windows 报告的访问接口名称完全匹配。 如果要使用提供程序名称进行匹配，则必须确保已在通过 Windows 开发人员中心硬件仪表板提交的服务元数据包中指定 CDMA 设备向 Windows 报告的提供程序名称的所有拼写和大小写形式。

 

### <a name="span-idmanaging_mvnosspanspan-idmanaging_mvnosspanspan-idmanaging_mvnosspanmanaging-mvnos"></a><span id="Managing_MVNOs"></span><span id="managing_mvnos"></span><span id="MANAGING_MVNOS"></span>管理 Mvno

可以使用以下三个选项之一来识别 CDMA 网络上的 Mvno。

**选项1： o 和 Mvno 获取其自己的 SID 值**

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 都获得唯一的 SID。 Mno 的 SID 值应该与每个 Mvno 的 SID 值不同。

为 o 以及设备向 Windows 报告的唯一 SID 值匹配的每个 Mvno 创建单独的服务元数据。

*图7基于 SID 的 CDMA 网络的匹配* 示例显示了从 WMIS 服务请求服务元数据的计算机的示例，以及来自客户端的每个匹配请求如何与体验相匹配。

![基于 sid 的匹配](images/hck-winb-fig5-sid-based-matching-matchingservicemetadata.jpg)

*图 7 CDMA 网络的基于 SID 的匹配*

-   计算机 \# 1 的匹配请求匹配 o 的 SID。 下载 o 服务元数据。

-   PC \# 2 的匹配请求与任何 SID 值或任何提供程序名称值都不匹配。 不会下载任何体验。

-   PC \# 3 的匹配请求与另一个 o 或 MVNO 定义的 SID 值匹配。

-   PC \# 4 的匹配请求与 MVNO MVNO b 的服务元数据的 SID 相匹配。

**选项2： o 和 Mvno 获取其自己的提供程序名称值**

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 设备报告一个提供程序名称值，该值唯一地标识 MVNO。 O 应具有其自己的提供程序名称值，以唯一标识它。

将为 o 和与设备向 Windows 报告的访问接口名称值匹配的每个 Mvno 创建单独的服务元数据。

要使此选项正常运行，o 必须确保未提交与设备报告的 SID 匹配的服务元数据。 如果这些 Sid 存在服务元数据，则会对 SID （而不是提供程序名称）执行匹配，从而导致此方案中断。 若要从 WMIS 中删除基于 SID 的元数据包，必须与 Windows 开发人员中心硬件仪表板支持联系。

*图 8 CDMA 网络的基于提供程序名称的匹配* 示例显示了从 Windows 元数据和 Internet 服务请求服务元数据 (WMIS) 服务的设备的示例，以及如何将设备的每个匹配请求与体验进行匹配。

![基于提供程序名称的匹配](images/hck-winb-fig6-provider-name-based-matching-matchingservicemetadata.jpg)

*图 8 CDMA 网络的基于提供程序名称的匹配*

-   PC \# 1 的匹配请求与 SID 不匹配，但与 o 的提供程序名称匹配。 下载 o 服务元数据。

-   PC \# 2 的匹配请求与任何 SID 值或任何提供程序名称值都不匹配。 不会下载任何体验。

-   PC \# 3 的匹配请求与另一个 o 或 MVNO 定义的 SID 值匹配。

-   \#在 SID 上，PC 4 的匹配请求不匹配，但与 MVNO B 的提供程序名称匹配。下载 MVNO B 的服务元数据。

**选项3：替换匹配方法**

如果此处所述的前两个选项不是可接受的，则 CDMA 操作员可以使用 "GSM 网络匹配" 部分的 " **选项7：备用匹配方法** " 中所述的替代匹配方法。

## <a name="span-idradiosspanspan-idradiosspanradios-and-metadata"></a><span id="radios"></span><span id="RADIOS"></span>无线收发器和元数据


您可以预期以下匹配行为，具体取决于无线电类型。

### <a name="span-idsingle-mode_single-subscription_devicespanspan-idsingle-mode_single-subscription_devicespanspan-idsingle-mode_single-subscription_devicespansingle-mode-single-subscription-device"></a><span id="Single-Mode_Single-Subscription_Device"></span><span id="single-mode_single-subscription_device"></span><span id="SINGLE-MODE_SINGLE-SUBSCRIPTION_DEVICE"></span>单模式单一订阅设备

单模式单一订阅设备是仅限 GSM 或仅 CDMA 的设备。 这些是通常可用的设备，只提供对 GSM 或 CDMA 网络的访问。

此设备向 Windows 报告 GSM 或 CDMA 模式。 上述匹配逻辑适用，并且设备与相应的服务元数据匹配。

### <a name="span-idmulti-mode_single-subscription_devicespanspan-idmulti-mode_single-subscription_devicespanspan-idmulti-mode_single-subscription_devicespanmulti-mode-single-subscription-device"></a><span id="Multi-Mode_Single-Subscription_Device"></span><span id="multi-mode_single-subscription_device"></span><span id="MULTI-MODE_SINGLE-SUBSCRIPTION_DEVICE"></span>多模式单一订阅设备

多模式单一订阅设备具有 GSM 和 CDMA 功能。 例如，可以通过对该操作员使用单个订阅者订阅来连接到 GSM LTE 网络或 CDMA 网络。

此设备将 GSM 报告为 Windows 的主模式。

当匹配此类设备的服务元数据时，可以创建与设备的 GSM 属性匹配的基于 GSM 的元数据。

### <a name="span-idsingle-mode_multi-subscription_devicespanspan-idsingle-mode_multi-subscription_devicespanspan-idsingle-mode_multi-subscription_devicespansingle-mode-multi-subscription-device"></a><span id="Single-Mode_Multi-Subscription_Device"></span><span id="single-mode_multi-subscription_device"></span><span id="SINGLE-MODE_MULTI-SUBSCRIPTION_DEVICE"></span>单模式多订阅设备

单模式多订阅设备一次可以有 GSM 或 CDMA 功能，并且它可以与多个提供商合作。 用户必须具有每个提供程序的订阅，才能使用多个提供程序。 例如，Qualcomm 戈壁芯片组允许用户连接到各种 CDMA 网络或 GSM 网络。

此设备将向 Windows 报告活动提供程序的模式。 如果设备与 GSM 提供程序处于活动状态，则应报告它处于 GSM 模式。 在这种情况下，应创建 GSM 元数据以进行匹配。 仅当设备处于 GSM 模式时，GSM 元数据和移动运营商应用才能访问设备。

如果设备在 CDMA 提供程序中处于活动状态，则它应报告该设备在 Windows 中处于 CDMA 模式。 在这种情况下，运算符应创建 CDMA 元数据以进行匹配。 仅当 CDMA metadata 和 mobile 宽带应用处于 CDMA 模式并且该 CDMA 网络处于活动状态时，才可访问该设备。

## <a name="span-idmetadatamtcspanspan-idmetadatamtcspanmetadata-maintenance-implications"></a><span id="metadatamtc"></span><span id="METADATAMTC"></span>元数据维护含义


重要的是要使以下元数据包内容保持最新：

-   包的说明方式。

-   与包匹配的 IMSI 和/或 ICCID 或 CDMA 提供程序名称或 SID 值。

有关移动宽带元数据的详细信息，请参阅 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

 

