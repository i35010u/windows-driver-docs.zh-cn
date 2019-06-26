---
title: 适用于 MVNO 的传送体验
description: 适用于 MVNO 的传送体验
ms.assetid: fcb2a3d4-bc19-4fa5-b81d-b0df287404a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e449dad173c6471002fa1a241b8a21f188d95045
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380968"
---
# <a name="delivering-experiences-for-mvnos"></a>适用于 MVNO 的传送体验

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

本主题提供有关如何匹配到移动网络运营商 (MNO) 或移动虚拟网络运营商 (MVNO) 的服务元数据，以便移动宽带设备插入时，会自动下载的移动宽带应用程序的信息。

若要成功匹配服务元数据，Windows SIM 卡插入到计算机中读取信息。 对于 CDMA 网络，读取移动宽带设备本身。 Windows 会查询 Windows 元数据和 Internet 服务 (WMIS) 数据库，若要下载正确的服务元数据包。 下载服务元数据包后，Windows 会将关联的移动宽带应用下载到计算机。

使用从以下列表适用于你的网络链接：

-   [GSM 网络进行匹配](#matching-on-gsm-networks)

-   [匹配上 CDMA 网络](#matching-on-cdma-networks)

有关正确匹配到 m n O 和 MVNO 服务元数据所需的硬件的信息，请参阅[移动运营商硬件概述](mobile-operator-hardware-overview.md)。

服务元数据的信息，请参阅[服务元数据](service-metadata.md)。

服务元数据包架构的信息，请参阅[服务的元数据数据包架构参考](service-metadata-package-schema-reference.md)。

## <a name="matching-on-gsm-networks"></a>GSM 网络进行匹配


对于 GSM 网络 (3GPP)，Windows SIM 卡从读取集成电路卡标识符 (ICCID) 和国际移动 (IMSI) 号。 这些数字必须设置并可从设备检索。 如果 SIM 是 PIN 锁定和隐藏 IMSI 信息，Windows 将不会操作，直到 SIM PIN 解锁。 Windows 还从 SIM 或移动宽带设备读取主页提供程序名称。

ICCID、 IMSI 和主页提供程序名称都可以从该设备，如果 ICCID 和 IMSI 是去掉最后两位数字，使用哈希算法，编码，并发送到的硬件 Id (HWIDs) 形式的 WMIS 以匹配服务元数据包。 主页提供程序名称进行检查。 如果没有匹配项，则检查 ICCID。 如果没有匹配项，则检查 IMSI。 如果不找到任何匹配项，不下载任何服务元数据包。 Windows 会大约每隔八天检查，以查看有关用户的移动宽带 SIM 是否存在新的元数据。

### <a name="span-idmanagingmvnosspanspan-idmanagingmvnosspanspan-idmanagingmvnosspanmanaging-mvnos"></a><span id="Managing_MVNOs"></span><span id="managing_mvnos"></span><span id="MANAGING_MVNOS"></span>管理 Mvno

如果你是对所有客户中有一个品牌 MNO，可以创建元数据包的 MCC + mnc 涵盖所有 IMSI 范围。 例如，如果 MCC + mnc 123 456，可以创建涵盖 123456000000000 – 123456999999999 元数据包。 这意味着，任何用户都将插入 SIM 在于范围匹配到你的体验。

这一点可能会更复杂，如果一个或多个 Mvno 共享相同的 MCC + mnc 值。 下面介绍了有关这种情况下处理策略。

**选项 1：分段 IMSI 范围**

使用此选项，m n O 不在服务元数据包，定义 ICCID 范围，并改为段出定义 m n O 体验和 MVNO 体验 IMSI 范围。 如果匹配的请求来自客户端设备，其 IMSI 值用于匹配到该 SIM 的正确体验。

此方法要求 m n O 可确保 IMSI 范围保持最新状态，并分配 Mvno 中可预测的 IMSI 编号块的未来范围。

如果 ICCID 和 IMSI 都不与匹配来自客户端计算机的请求，没有进行匹配。

**请注意**   IMSI 范围必须具有 100 个粒度。 起始范围值必须以 00，结束，99 结尾结束范围值。

 

*图 1 分段 IMSI 范围 （在 m n O MCC + mnc 是否）* 显示从 WMIS 和如何从客户端每个匹配的请求匹配到体验中请求服务元数据的客户端设备的示例。

![分段 imsi 范围](images/hck-winb-fig1-segmenting-imsi-ranges-matchingservicemetadata.jpg)

**图 1 分段 IMSI 范围 （以 m n O MCC + mnc)**

-   计算机\#匹配 1 的请求不与任何 ICCID 值和 m n O 定义 IMSI 范围内的着陆不匹配。 M n O 服务元数据下载到该计算机。

-   计算机\#2 的匹配请求不与任何 ICCID 值或任何 IMSI 值不匹配。 下载没有体验。

-   计算机\#3 的匹配请求和不匹配任何 ICCID 值在 IMSI 范围之内的着陆 MVNO aMVNO 服务元数据下载到该计算机。

**选项 2：分段 ICCID 范围**

使用此选项，m n O 不在服务元数据包，定义 IMSI 范围，并改为段出定义 m n O 体验和 MVNO 体验的 ICCID 范围。 如果匹配的请求来自客户端计算机，ICCID 值用于匹配到该 SIM 的正确体验。

此方法要求 m n O 可确保范围保持最新和 Mvno 分配可预测的 ICCID 数字块中的未来范围。 如果在 SIM 制造期间分配给 sims 就较大的 ICCIDs 块，这可以是 m n O 和其 Mvno 的理想匹配策略。

如果 ICCID 和 IMSI 都不匹配来自客户端计算机的请求，则进行没有匹配项。

**请注意**   IMSI 范围必须具有 100 个粒度。 起始范围值必须以 00，结束，99 结尾结束范围值。

 

*图 2 分段 ICCID 范围 （在 m n O ICCID 颁发者标识号）* 显示从 WMIS 和如何从客户端每个匹配的请求匹配到体验中请求服务元数据的计算机的客户端的示例。

![分段 iccid 范围](images/hck-winb-fig2-segmenting-iccid-ranges-matchingservicemetadata.jpg)

**图 2 分段 ICCID 范围 （在 m n O ICCID 颁发者标识）**

-   计算机\#1 的匹配请求中的包含由 m n O 的 ICCID 范围内。 M n O 服务元数据下载到该计算机。

-   计算机\#2 的匹配请求不与任何 ICCID 值或任何 IMSI 值不匹配。 下载没有体验。

-   计算机\#3 的匹配请求领土定义 MVNO a ICCID 范围内MVNO 服务元数据下载到该计算机。

**选项 3:IMSI 范围以及与 ICCID 范围和 m n O 描述 Mvno**

可以分配 MNO 整个基于 IMSI 的范围 （即下的所有内容及其 mnc 是否 MCC + 值）。 然后为分配任何 Mvno 其 sims 就有关的特定 ICCID 范围。 这意味着，除非存在 ICCID 匹配项，SIM SIM 获取 m n O 体验。

此选项要求 MNO 或 MVNO，以确保 ICCID 范围保持最新和 Mvno 分配可预测的 ICCID 数字块中的未来范围。 如果在 SIM 制造期间分配给 sims 就较大的 ICCIDs 块，这可以是 m n O 和其 Mvno 的理想匹配策略。 这意味着 m n O 具有较少的维护，因为其包跨所有基于 IMSI 的范围。 在此方案中，它是非常重要，以确保 MVNO 保留其 ICCID 范围最新。否则，可以匹配客户 MVNO m n O 体验。

**请注意**   IMSI 范围必须具有 100 个粒度。 起始范围值必须以 00，结束，99 结尾结束范围值。

 

*图 3 使用 ICCID 为 m n O 定义 Mvno 和全面 IMSI 范围*显示从 WMIS 和如何从客户端每个匹配的请求匹配到体验中请求服务元数据的计算机的客户端的示例。

![使用 iccid 定义 mvno](images/hck-winb-fig3-using-iccid-to-define-mvnos-matchingservicemetadata.jpg)

*图 3 使用 ICCID 为 m n O 定义 Mvno 和全面 IMSI 范围*

-   计算机\#匹配 1 的请求不与任何 ICCID 值和 m n O 定义 IMSI 范围内的着陆不匹配。 在该计算机上下载 m n O 服务元数据。

-   计算机\#2 的匹配请求中的包含 ICCID 范围内的 MVNO B.MVNO B 的服务元数据下载到该计算机。

-   计算机\#匹配 3 的 ICCID 范围中包含请求，对于 MVNO A.MVNO A 的服务元数据下载到该计算机。

-   计算机\#匹配 4 的请求不与任何 ICCID 值和 m n O 定义 IMSI 范围内的着陆不匹配。 在该计算机上下载 m n O 服务元数据。

**选项 4:分段 ICCID 和 IMSI 范围**

可以使用混合使用 ICCID 范围和 IMSI 范围来描述的 m n O 和 MVNO 网络。

**请注意**   ICCID 范围获取第一个匹配的优先级。

 

这是最复杂的匹配模型。 若要确保正确匹配，m n O 和 MVNO 都必须频繁地更新其服务元数据包。

*图 4 分段 ICCID 和 IMSI 范围*显示从 WMIS，以及如何从客户端每个匹配的请求匹配到体验中请求服务元数据的客户端设备的示例。

![分段 ccid 和 imsi 范围](images/hck-winb-fig4-segmenting-ccid-and-imsi-ranges-matchingservicemetadata.jpg)

*图 4 分段 ICCID 和 IMSI 范围*

-   计算机\#匹配 1 的请求不匹配任何 ICCID 值，但包含在由 m n O IMSI 范围。 M n O 服务元数据下载到该计算机。

-   计算机\#2 的匹配 MVNO B.MVNO B 的服务元数据下载到该计算机，ICCID 范围中包含的请求。

-   计算机\#匹配 3 的 ICCID 范围中包含请求，对于 MVNO A.MVNO A 的服务元数据下载到该计算机。

-   计算机\#匹配 4 的请求不匹配任何 ICCID 值，但包含在由 m n O IMSI 范围。 M n O 服务元数据下载到该计算机。

-   计算机\#5 的匹配请求不匹配任何 ICCID 值，但包含在 IMSI 范围定义的 MVNO C.MVNO C 的服务元数据下载到该计算机的作用。

**选项 5:使用主页 GSM 网络提供程序名称标识的 m n O 和 MVNO**

使用此选项，m n O 不在服务元数据包，定义 IMSI 或 ICCID 范围和段改为 out 主页提供程序名称，以规定 m n O 体验和 MVNO 体验。

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 设备报告提供程序名称值，用于唯一地标识 MVNO。 M n O 应具有唯一标识其自己的提供程序名称值。

如果匹配的请求来自客户端计算机，主页提供程序名称用于匹配到该 SIM 的正确体验。

建议仅在 IMSI 和 ICCID 无法使用这种情况中使用此选项。

主页提供程序名称与来自客户端计算机的请求不匹配，如果没有进行匹配。

**请注意**  主页的提供程序名称必须全局唯一，以确保用户获取正确的体验。 服务元数据将只允许使用给定的主页提供程序名称的单个服务的元数据包。

 

*图 5 基于提供程序名称匹配的 GSM 网络*显示从 Windows 元数据和 Internet 服务 (WMIS) 服务和如何从设备每个匹配的请求匹配到请求服务元数据的设备的示例体验。

![使用 gsm 网络的家庭的提供程序名称](images/hck-winb-fig5-using-home-provider-name-for-gsm-networks-to-identify-the-mno-and-mvno.jpg)

*图 5 基于提供程序名称匹配的 GSM 网络*

-   计算机\#1 的匹配请求匹配的 MNO 主页提供程序名称。 下载 m n O 服务元数据。

-   计算机\#2 的匹配请求与任何提供程序名称的值不匹配。 下载没有体验。

-   计算机\#3 的匹配请求匹配项下载为 MVNO A.MVNO A 的服务元数据主页提供程序名称。

-   计算机\#4 的匹配请求匹配项下载为 MVNO B.MVNO B 的服务元数据主页提供程序名称。

**选项 6:IMSI 范围以及描述 Mvno 主页提供程序名称与 m n O**

可以分配 MNO 整个基于 IMSI 的范围 （即下的所有内容及其 mnc 是否 MCC + 值）。 然后可以分配任何 Mvno 特定主页提供程序名称。 这意味着除非主页提供程序名称匹配，则为该设备，设备获取 m n O 体验。

此选项需要以确保报告使用的主页提供程序名称从设备不会更改的 MNO 或 MVNO，是全局唯一保持为最新。 建议仅在 IMSI 和 ICCID 无法使用这种情况中使用此选项。

*图 6 使用主页提供程序名称，用于定义 Mvno 和全面 IMSI 范围为 m n O*显示从 WMIS 和如何从客户端每个匹配的请求匹配到体验中请求服务元数据的计算机的客户端的示例。

![使用家庭的提供程序名称来定义 mvno](images/hck-winb-fig6-using-home-provider-name-to-define-mvnos-and-an-all-encompassing-imsi-range-for-the-mno.jpg)

*图 6 使用主页提供程序名称为 m n O 定义 Mvno 和全面 IMSI 范围*

-   计算机\#1 的匹配请求匹配 MVNO a 主页提供程序名称在该计算机上下载 MVNO 的服务元数据。

-   计算机\#2 的匹配请求不与任何主页提供程序名称值和 m n O 定义 IMSI 范围内的着陆不匹配。 在该计算机上下载 m n O 服务元数据。

-   计算机\#3 的匹配主页提供程序名称为 MVNO B.MVNO B 的服务元数据下载到该计算机的请求匹配项。

-   计算机\#匹配 4 的请求不与任何主页提供程序名称值和 m n O 定义 IMSI 范围内的着陆不匹配。 在该计算机上下载 m n O 服务元数据。

**选项 7:替代匹配的方法**

如果这些方法均不适用于 m n O 的网络 （例如，m n O 不能跟踪的 m n O 的和 MVNO 的客户之间的 IMSI 和 ICCID 范围），以下替代方法是可用。 它比任何上文所述的选项不太理想，但对于在网络上的 Windows 8、 Windows 8.1 或 Windows 10 客户提供移动宽带解决方案。

**服务元数据**

此方法创建涵盖整个 m n O 网络服务元数据包。 这通常是通过将提交一个 IMSI 范围，涵盖了 m n O 网络上的所有 MCC + mnc 值和无 ICCID 范围。 未描述 MVNO 范围。 服务元数据包的功能一般品牌以及显示 Windows 连接管理器中的通用网络名称。 然后，服务元数据引用检测到 m n O 的 SIM 时自动下载从 Microsoft Store 的泛型应用程序。

**确定网络隶属关系**

如果用户尚不包含一个计划，当用户尝试使用 Windows 连接管理器连接到网络时打开应用。

当运行该应用程序时，它执行以下操作之一：

-   提示用户识别他们具有计划从显示的列表的 Mvno 网络、 MNO 网络。

-   使用 web 服务可以将有关用户的 sim 卡信息发送回 m n O 后端，这样的操作员可以使用自定义逻辑来确定正确的网络适用于用户的品牌。

**自定义 Windows 连接管理器品牌**

用户的移动宽带数据之后计划隶属关系确定，移动宽带应用程序可以更改显示 Windows 连接管理器中的徽标和网络名称。 这是通过使用预配元数据，使运营商应用程序，将基于 XML 的信息发送给与特定订阅者的计划信息的 Windows 帐户。

有关帐户设置的详细信息，请参阅[帐户预配](account-provisioning.md)。

**服务元数据更新**

将来的服务元数据更新 （例如，提交到通用服务元数据包的任何更改） 可以覆盖订阅服务器的计算机上应用的品牌。 若要避免此问题，我们建议，如果可能，将不会更新服务元数据包。 因为元数据包包含泛型品牌，并包括 m n O 整个 IMSI 范围，不应经常需要更新用于此方案中的包。

如果必须更新服务元数据包，请确保移动宽带应用可以启动另一个帐户预配基于运算符提供后端逻辑的元数据操作。 这样一来，可以指定服务元数据更新在后端，并具有定期检查后端和应用帐户预配所需的元数据信息的应用。

**请注意**  服务元数据未进行版本控制的因为该应用程序无法查询元数据以确定它是否具有已更新或通过使用帐户预配的元数据所做的自定义将对应用的本地副本。 没有用于唤醒并应用于计算机的服务元数据更新响应的应用的方法。

通过 Windows 开发人员中心硬件仪表板中上, 传服务元数据的时间，计算机将收到更新的元数据的时间之间可能发生延迟。

 

**品牌的移动宽带应用中**

重塑品牌 Windows 连接管理器图标和 m n O/MVNO 的网络的网络名称可以使用本主题中描述的上一步骤。 但是，有有限的方式在其中应用本身可以产品名称更改。

您可以重塑品牌的应用中的以下项：

-   应用程序内容本身 （即，应用程序内的所有内容可更改为某一特定运算符）。 这是对其应用程序具有完全控制代码。 可能想要更改帮助内容、 导航选项、 页面布局、 颜色和品牌内部应用程序中，基于 m n O/MVNO。

-   可以动态更新应用程序磁贴以显示特定映像和特定于该运算符的布局。 有关如何动态更新磁贴内容的信息，请参阅[快速入门：发送磁贴更新](https://docs.microsoft.com/previous-versions/windows/apps/hh465439(v=win.10))。

不能重塑品牌的应用中的以下项：

-   应用的名称。 可以尝试通过更改磁贴模板，隐藏名称，但因为它应用程序清单中定义不能更改名称本身或代表该应用的图标。

-   应用名称、 信息和设置超级按钮中的图标。

-   应用的说明。

### <a name="span-idsimreprogrammingspanspan-idsimreprogrammingspanspan-idsimreprogrammingspansim-reprogramming"></a><span id="SIM_reprogramming"></span><span id="sim_reprogramming"></span><span id="SIM_REPROGRAMMING"></span>SIM 重新编程

如果你想要动态对 sims 就更改 IMSI 或 ICCID 重新编程，您应注意下列任一方法在其中 Windows 8、 Windows 8.1 和 Windows 10 解释重新编程：

-   重新编程要求设备的 IMSI 和 ICCID 的缓存的失效。 有几种方法进行这种，具体取决于运营商网络和设备。

-   囿 SIM 后，设备将重新读取 sim 卡信息。 它可以使用热 SIM 交换插入序列让 Windows 知道它应重新查询新的 IMSI 和 ICCID 值。

-   必须更改 ICCID 或 Windows 将不被视为 SIM 新 SIM。

-   如果仅更改 IMSI，Windows 不会视为 SIM 新 SIM 和不下载服务元数据。 如果已为此 sim 卡中下载了不同的应用，不被下载的移动宽带应用。

若要获取新服务的元数据 （这会导致新品牌），并获取新的移动宽带应用下载 ICCID 和 IMSI，则必须更改服务数据和通过使用运算符的移动宽带应用的重新编程方法。

## <a name="matching-on-cdma-networks"></a>匹配上 CDMA 网络


对于 CDMA 网络 (3GPP2)，Windows 将读取 SID，向相应的服务元数据包 WMIS 中报告的设备的提供程序名称值。 如果不找到任何匹配项，不下载任何服务元数据包。 Windows 会大约每隔八天检查，以查看设备是否存在新的元数据。 如果存在的 sid 的服务元数据和单独的服务元数据包存在对于提供程序名称，并且这两个值与设备报告的 SID 和提供程序名称值匹配，匹配的首选项提供给 SID。 在这种情况下，提供程序名称包不匹配。

**重要**  提供程序名称值是区分大小写，并且必须与提供程序到 Windows 设备报告的名称完全匹配。 如果你想要通过使用提供程序名称匹配，则必须确保指定所有的提供程序名称的拼写和大小写变体 CDMA 设备报告给 Windows 中通过 Windows 开发人员中心提交服务元数据包硬件仪表板。

 

### <a name="span-idmanagingmvnosspanspan-idmanagingmvnosspanspan-idmanagingmvnosspanmanaging-mvnos"></a><span id="Managing_MVNOs"></span><span id="managing_mvnos"></span><span id="MANAGING_MVNOS"></span>管理 Mvno

可以通过使用以下三个选项之一标识 Mvno CDMA 网络上。

**选项 1：M n O 和 Mvno 获取其自己的 SID 值**

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 获取一个唯一的 SID。 Mno 应具有其自己不同于每个 Mvno 的 SID 值。

为 m n O 和每 Mvno 上设备报告给 Windows 的唯一 SID 值的匹配，则会创建单独的服务元数据。

*图 7 基于 SID 匹配的 CDMA 网络*显示从 WMIS 服务，以及如何获取客户端从每个匹配的请求匹配到体验中请求服务元数据的计算机的示例。

![基于 sid 的匹配](images/hck-winb-fig5-sid-based-matching-matchingservicemetadata.jpg)

*图 7 基于 SID 匹配的 CDMA 网络*

-   计算机\#1 的匹配的 MNO 的请求匹配的 SID。 下载 m n O 服务元数据。

-   PC \#2 的匹配请求不匹配的 SID 的任何值或任何提供程序名称值。 下载没有体验。

-   PC \#3 的匹配请求与定义的另一个的 MNO 或 MVNO SID 值相匹配。

-   PC \#4 的匹配请求匹配的 SID MVNO B.MVNO B 的服务元数据下载。

**选项 2：M n O 和 Mvno 获取自己的提供程序名称值**

对于分配给 Mvno 的移动宽带设备，请确保每个 MVNO 设备报告提供程序名称值，用于唯一地标识 MVNO。 M n O 应具有唯一标识其自己的提供程序名称值。

M n O 和每个设备报告给 Windows 的提供程序名称值匹配 Mvno，会创建单独的服务元数据。

若要运行此选项，m n O 必须确保不提交在 SID 与匹配的任何服务元数据时，设备报告。 如果服务元数据中存在这些 Sid，而不是提供程序名称，从而导致中断此方案的 SID 执行匹配项。 若要删除 WMIS 基于 SID 的元数据包，必须联系 Windows 开发人员中心硬件仪表板支持。

*图 8 基于提供程序名称的匹配 CDMA 网络*显示从 Windows 元数据和 Internet 服务 (WMIS) 服务和如何从设备每个匹配的请求匹配到请求服务元数据的设备的示例体验。

![基于提供程序名称匹配](images/hck-winb-fig6-provider-name-based-matching-matchingservicemetadata.jpg)

*图 8 基于提供程序名称的匹配 CDMA 网络*

-   PC\#匹配 1 的请求不匹配的 SID，但与 m n O 提供程序名称匹配。 下载 m n O 服务元数据。

-   PC \#2 的匹配请求不匹配的 SID 的任何值或任何提供程序名称值。 下载没有体验。

-   PC \#3 的匹配请求与定义的另一个的 MNO 或 MVNO SID 值相匹配。

-   PC\#匹配 4 的请求不匹配的 SID，但与 MVNO B 的提供程序名称下载 MVNO B 的服务元数据。

**选项 3:替代匹配的方法**

如果不接受此处所述的前两个选项的 CDMA 操作员可以使用的匹配中所述的方法的替代方案**选项 7:匹配方法的替代方法**GSM 上匹配的网络部分。

## <a name="span-idradiosspanspan-idradiosspanradios-and-metadata"></a><span id="radios"></span><span id="RADIOS"></span>无线收发器和元数据


您可以预计以下匹配行为，具体取决于广播的类型。

### <a name="span-idsingle-modesingle-subscriptiondevicespanspan-idsingle-modesingle-subscriptiondevicespanspan-idsingle-modesingle-subscriptiondevicespansingle-mode-single-subscription-device"></a><span id="Single-Mode_Single-Subscription_Device"></span><span id="single-mode_single-subscription_device"></span><span id="SINGLE-MODE_SINGLE-SUBSCRIPTION_DEVICE"></span>单模式单一订阅设备

单模式单个订阅设备是仅限 GSM 的或仅限 CDMA 的设备。 这些是提供仅 GSM 或 CDMA 网络访问权限的常用设备。

此设备报告给 Windows GSM 或 CDMA 模式。 前面所述的匹配逻辑应用，并在设备与相应的服务元数据匹配。

### <a name="span-idmulti-modesingle-subscriptiondevicespanspan-idmulti-modesingle-subscriptiondevicespanspan-idmulti-modesingle-subscriptiondevicespanmulti-mode-single-subscription-device"></a><span id="Multi-Mode_Single-Subscription_Device"></span><span id="multi-mode_single-subscription_device"></span><span id="MULTI-MODE_SINGLE-SUBSCRIPTION_DEVICE"></span>多模式单一订阅设备

多模式单个订阅设备具有 GSM 和 CDMA 功能。 例如，它可以连接到 GSM LTE 网络或 CDMA 网络通过单个订阅者订阅用于该运算符。

此设备所报告的主模式到 Windows GSM。

在匹配服务元数据对于此类型的设备时，可以创建基于 GSM 的元数据相匹配的设备 GSM 属性。

### <a name="span-idsingle-modemulti-subscriptiondevicespanspan-idsingle-modemulti-subscriptiondevicespanspan-idsingle-modemulti-subscriptiondevicespansingle-mode-multi-subscription-device"></a><span id="Single-Mode_Multi-Subscription_Device"></span><span id="single-mode_multi-subscription_device"></span><span id="SINGLE-MODE_MULTI-SUBSCRIPTION_DEVICE"></span>单模式多订阅设备

单模式多订阅设备都可以一次有 GSM 或 CDMA 功能活动，它就能使用多个提供程序。 用户必须具有从每个提供程序以使用多个提供程序订阅。 例如，Qualcomm 戈壁芯片集允许用户连接到各种 CDMA 网络或 GSM 网络。

此设备向 Windows 中报告模式下，为活动提供程序。 如果设备处于活动状态，且 GSM 提供程序，它应该报告处于 GSM 模式。 在这种情况下，应创建用于匹配 GSM 元数据。 GSM 元数据和移动运营商应用程序可以访问设备时在 GSM 模式下。

如果设备处于活动状态，具有 CDMA 提供程序，它应该报告处于 CDMA 模式设置为 Windows。 在这种情况下，操作员应创建用于匹配 CDMA 元数据。 CDMA 元数据和移动宽带应用可以访问该 CDMA 网络设备在 CDMA 模式下时唯一且处于活动状态。

## <a name="span-idmetadatamtcspanspan-idmetadatamtcspanmetadata-maintenance-implications"></a><span id="metadatamtc"></span><span id="METADATAMTC"></span>元数据维护的意义


请务必使以下元数据包内容保持最新：

-   如何描述包。

-   IMSI 和/或 ICCID 或 CDMA 提供程序名称或对其包匹配的 SID 值。

有关移动宽带元数据的详细信息请参阅[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

 

 





