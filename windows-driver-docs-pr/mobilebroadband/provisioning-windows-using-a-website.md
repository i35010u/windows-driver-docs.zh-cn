---
title: 使用网站预配 Windows
description: 使用网站预配 Windows
ms.assetid: ba60fddd-a248-4afb-9390-f9277ef1f094
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99777210008f6aaa9c7684f5162fcef16e8ad50c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369218"
---
# <a name="provisioning-windows-using-a-website"></a>使用网站预配 Windows


本主题介绍如何使用网站让客户购买和设置移动宽带计划运行的 Windows 8、 Windows 8.1 或 Windows 10 的计算机上。

有关 Windows 8、 Windows 8.1 和 Windows 10 中的移动宽带的详细信息，请参阅[的移动宽带概述](overview-of-mobile-broadband.md)。

我们建议您开发并使用移动宽带应用，因为它提供了最大的灵活性和创建最集成的体验。 但是，在几个计划中购买和设置情况下，移动宽带应用并不一定是已安装并可供使用。 对于这些情况下，Windows 8、 Windows 8.1 和 Windows 10 包括支持，以自动打开移动宽带的网站，由你托管并提供完成这些方案所需的体验。

## <a name="span-idkeyscenspanspan-idkeyscenspankey-scenarios-that-require-a-mobile-broadband-web-site"></a><span id="keyscen"></span><span id="KEYSCEN"></span>需要移动宽带网站的关键方案


下面的方案需要移动宽带网站：

-   [首次使用一个 USB 调制解调器](#firstusb)

-   [首次使用嵌入的调制解调器以及 SIM](#firstsimusb)

-   [计划续订时卸载应用](#renewunin)

### <a name="span-idfirstusbspanspan-idfirstusbspanfirst-use-of-a-usb-modem"></a><span id="firstusb"></span><span id="FIRSTUSB"></span>首次使用一个 USB 调制解调器

用户启动与 Windows 8、 Windows 8.1 或 Windows 10 认证移动宽带 USB 调制解调器没有活动关联的数据计划。 用户第一次，将 USB 调制解调器连接到 Windows 8、 Windows 8.1 或 Windows 10 计算机和移动宽带类驱动程序会自动安装的设备。 用户打开 Windows 连接管理器，并选择要连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不会不提供 Internet 访问，因为没有活动的数据计划与设备相关联。 通常情况下，Windows 将打开移动宽带应用程序，以便应用程序可以提供用于购买数据计划或否则启用 Internet 访问的选项。 但是，由于只需安装 USB 调制解调器，移动宽带应用尚未安装在计算机上。

在这种情况下，Windows 将打开由你提供一个网站。 此网站提供了购买数据计划或否则启用 Internet 访问的功能。 体验完成后，数据计划程序与 USB 调制解调器和计算机授予移动宽带网络上的 Internet 访问。

### <a name="span-idfirstsimusbspanspan-idfirstsimusbspanfirst-use-of-a-sim-with-an-embedded-modem"></a><span id="firstsimusb"></span><span id="FIRSTSIMUSB"></span>首次使用与嵌入的调制解调器 SIM

用户启动使用不具有活动关联的数据计划 SIM。 用户将 sim 卡插入到具有嵌入的移动宽带调制解调器的 Windows 8、 Windows 8.1 或 Windows 10 计算机。 用户打开 Windows 连接管理器，并选择要连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不会因为没有活动的数据计划与 sim 卡关联提供 Internet 访问权限。 通常情况下，Windows 将打开移动宽带应用程序，以便应用程序可以提供用于购买数据计划或否则启用 Internet 访问的选项。 但是，因为只需插入 sim 卡，移动宽带应用尚未安装在计算机上。

在这种情况下，Windows 将打开由你提供一个网站。 此网站提供了购买数据计划或否则启用 Internet 访问的功能。 体验完成后，数据计划程序与 SIM 和计算机授予移动宽带网络上的 Internet 访问。

### <a name="span-idrenewuninspanspan-idrenewuninspanplan-renewal-when-the-app-has-been-uninstalled"></a><span id="renewunin"></span><span id="RENEWUNIN"></span>计划续订时卸载应用

用户具有已定期使用移动宽带 Windows 8、 Windows 8.1 或 Windows 10 计算机上。 在某些时候，用户卸载的移动宽带应用和数据计划由于过期日期或数据使用情况已过期。 用户打开 Windows 连接管理器，并选择要连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不因为不再与设备相关联的活动数据计划提供 Internet 访问权限。

由于 Windows 无法启动已卸载应用程序，Windows 将打开由你提供一个网站。 在此网站上，提供续订用户的数据计划或否则启用 Internet 访问的体验。 体验完成后，数据计划程序再次与用户的设备和计算机授予移动宽带网络上的 Internet 访问。

## <a name="span-idhowtoenablekeyscenariosspanspan-idhowtoenablekeyscenariosspanspan-idhowtoenablekeyscenariosspanhow-to-enable-key-scenarios"></a><span id="How_to_enable_key_scenarios"></span><span id="how_to_enable_key_scenarios"></span><span id="HOW_TO_ENABLE_KEY_SCENARIOS"></span>如何启用关键方案


使用以下准则来帮助你启用这些重要方案。

### <a name="span-idenablesimpspanspan-idenablesimpspanenable-a-simple-connect-experience"></a><span id="enablesimp"></span><span id="ENABLESIMP"></span>启用简单的连接体验

必须提供最少量的数据要包含在 Windows 8、 Windows 8.1 或 Windows 10 APN 数据库中。 有关 Windows APN 数据库的详细信息，请参阅[APN 数据库概述](apn-database-overview.md)。

必须提供要包括在 APN 数据库中的以下信息：

-   对于 Windows，而无需用户输入一个 APN 或访问字符串连接到移动宽带网络，你必须提供 APNs 和/或访问字符串。

-   对于 Windows 检测到没有 Internet 连接时自动打开移动宽带网站，您必须提供网站的 URL。

### <a name="span-iddetectspanspan-iddetectspandetect-internet-access"></a><span id="detect"></span><span id="DETECT"></span>检测 Internet 访问权限

当 Windows 首次连接到网络，以确定 Internet 连接时，它将执行各种网络测试。 这些测试的目标站点是 msftncsi.com，它是专门用于连接测试保留的域。

若要避免误报或假负，你的网络必须允许访问 www.msftncsi.com ，仅当用户具有常规 Internet 访问。 无活动的数据计划连接到网络的用户不能对 www.msftncsi.com 的访问。

### <a name="span-idwebaccessspanspan-idwebaccessspanweb-site-access"></a><span id="webaccess"></span><span id="WEBACCESS"></span>网站的访问

移动运营商通常会限制网络访问的用户不具有活动的数据计划通过使用两种方法之一：

-   用户保持在相同的 APN，但阻止访问所有网络目标所需的计划购买和激活的服务器的最小集除外。 此实现中也称为是"围墙的花园"。

-   转换到购买 APN 永远不会提供 Internet 访问权限，用户但可提供所需的计划购买和激活的服务器的集访问权限。

没有活动的数据计划的用户必须能够通过使用下列方法之一访问移动宽带 web 站点。 此外，用户必须能够通过使用 HTTPS 连接通过 Internet 访问 web 站点。

### <a name="span-iddevinfspanspan-iddevinfspandevice-information"></a><span id="devinf"></span><span id="DEVINF"></span>设备信息

当 Windows 使用移动运营商的 URL (AccountExperienceURL 属性中的[运算符](operator.md)元素) 从 APN 数据库中，Windows 提供了所需以完成激活到移动宽带设备信息web 站点。 此设备信息作为 HTTPS 请求的参数传递到 web 站点。

URL 的格式是 **https://Operator URL\[ ？ propN = valN\[ & propN = valN\]\*\]** ，其中：

-   **运算符 URL** URL 由你提供并且存储在 APN 数据库

-   **propN**属性名称。

-   **valN**为属性名称的相应值。

下表列出了可以包含的属性。 如果属性值未提供移动宽带设备，则不包含该属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SubId</p></td>
<td><p>订阅者 ID</p>
<ul>
<li><p>对于 GSM 设备：IMSI （最多为 15 个数字）</p></li>
<li><p>对于 CDMA 设备：最小值或 MIN(IRM) （10 位数）</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DevId</p></td>
<td><p>设备 ID</p>
<ul>
<li><p>对于 GSM 设备：IMEI （最多为 15 个数字）</p></li>
<li><p>对于 CDMA 设备：ESN （11 位数字） 或 MEID （17 位）</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IccId</p></td>
<td><p>SIM ICCID （19 20 位数字）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idconfigurethecomputerspanspan-idconfigurethecomputerspanspan-idconfigurethecomputerspanconfigure-the-computer"></a><span id="Configure_the_computer"></span><span id="configure_the_computer"></span><span id="CONFIGURE_THE_COMPUTER"></span>将计算机配置

用户已购买数据计划，或以其他方式使用网站上激活移动宽带设备后，可能需要对计算机进行以下配置更改：

-   定义移动宽带连接配置文件

-   提供帐户数据

-   定义的 Wi-fi 热点连接配置文件

-   指示计算机重新连接移动宽带设备

此外可以由移动宽带网站应用相同的帐户预配使用移动宽带应用应用到计算机的元数据。 在 web 页面的 JavaScript 中，检查的可用性[ **window.external.msProvisionNetworks** ](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85))方法。 如果存在，则在浏览器可以传输帐户预配到 Windows 元数据。

帐户预配的元数据的详细信息，请参阅[帐户预配](account-provisioning.md)。

**请注意**  帐户预配的元数据必须使用由该网站提供的扩展的验证 (EV) 证书进行签名。

 

 

 





