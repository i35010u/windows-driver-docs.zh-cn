---
title: 使用网站预配 Windows
description: 使用网站预配 Windows
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ef6e9d4cf14523b74e299d431243c1760e4fe0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786185"
---
# <a name="provisioning-windows-using-a-website"></a>使用网站预配 Windows


本主题介绍如何使用网站让客户在运行 Windows 8、Windows 8.1 或 Windows 10 的计算机上购买和设置移动宽带计划。

有关 Windows 8、Windows 8.1 和 Windows 10 中的移动宽带的详细信息，请参阅 [移动宽带概述](overview-of-mobile-broadband.md)。

建议你开发和使用移动宽带应用，因为它提供了最大的灵活性并创建了最集成的体验。 但是，在某些计划购买和设置方案中，移动宽带应用程序可能不会始终安装并可供使用。 对于这些方案，Windows 8、Windows 8.1 和 Windows 10 包括自动打开由你托管的移动宽带网站的支持，并提供完成这些方案所需的体验。

## <a name="span-idkeyscenspanspan-idkeyscenspankey-scenarios-that-require-a-mobile-broadband-web-site"></a><span id="keyscen"></span><span id="KEYSCEN"></span>需要移动宽带网站的关键方案


以下方案需要移动宽带网站：

-   [第一次使用 USB 调制解调器](#firstusb)

-   [首次使用 SIM 和嵌入的调制解调器](#firstsimusb)

-   [应用卸载后计划续订](#renewunin)

### <a name="span-idfirstusbspanspan-idfirstusbspanfirst-use-of-a-usb-modem"></a><span id="firstusb"></span><span id="FIRSTUSB"></span>第一次使用 USB 调制解调器

用户开始时使用的是 Windows 8、Windows 8.1 或 Windows 10 认证的移动宽带 USB 调制解调器，该调制解调器没有活动的关联数据计划。 用户首次将 USB 调制解调器连接到 Windows 8、Windows 8.1 或 Windows 10 计算机，并为该设备自动安装移动宽带类驱动程序。 用户打开 Windows 连接管理器，并选择连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不提供 Internet 访问权限，因为没有活动的数据计划与设备相关联。 通常，Windows 会打开移动宽带应用程序，以便应用程序可以提供购买数据计划或启用 Internet 访问的选项。 但是，因为 USB 调制解调器刚刚安装，所以计算机上尚未安装移动宽带应用。

在这种情况下，Windows 将打开你提供的网站。 此网站提供购买数据计划或以其他方式启用 Internet 访问的功能。 完成此过程后，数据计划与 USB 调制解调器相关联，并且在移动宽带网络上授予计算机 Internet 访问权限。

### <a name="span-idfirstsimusbspanspan-idfirstsimusbspanfirst-use-of-a-sim-with-an-embedded-modem"></a><span id="firstsimusb"></span><span id="FIRSTSIMUSB"></span>首次使用带有嵌入的调制解调器的 SIM

用户以没有活动关联数据计划的 SIM 开头。 用户将 SIM 插入 Windows 8、Windows 8.1 或具有嵌入移动宽带调制解调器的 Windows 10 计算机。 用户打开 Windows 连接管理器，并选择连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不提供 Internet 访问权限，因为没有与 SIM 关联的活动数据计划。 通常，Windows 会打开移动宽带应用程序，以便应用程序可以提供购买数据计划或启用 Internet 访问的选项。 不过，由于 SIM 刚刚插入，因此该计算机上尚未安装移动宽带应用。

在这种情况下，Windows 将打开你提供的网站。 此网站提供购买数据计划或以其他方式启用 Internet 访问的功能。 经验完成后，数据计划与 SIM 相关联，并在移动宽带网络上向计算机授予 Internet 访问权限。

### <a name="span-idrenewuninspanspan-idrenewuninspanplan-renewal-when-the-app-has-been-uninstalled"></a><span id="renewunin"></span><span id="RENEWUNIN"></span>应用卸载后计划续订

用户在 Windows 8、Windows 8.1 或 Windows 10 计算机上经常使用 mobile 宽带。 某些时候，用户卸载了移动宽带应用程序，但数据计划由于过期日期或数据使用而过期。 用户打开 Windows 连接管理器，并选择连接到移动宽带网络。

作为连接过程的一部分，Windows 会确定移动宽带网络不提供 Internet 访问权限，因为活动数据计划不再与设备相关联。

由于 Windows 无法启动已卸载的应用程序，因此 Windows 将打开你提供的网站。 在此网站上，提供续订用户数据计划或启用 Internet 访问的体验。 经验完成后，数据计划再次与用户的设备关联，并在移动宽带网络上授予计算机 Internet 访问权限。

## <a name="span-idhow_to_enable_key_scenariosspanspan-idhow_to_enable_key_scenariosspanspan-idhow_to_enable_key_scenariosspanhow-to-enable-key-scenarios"></a><span id="How_to_enable_key_scenarios"></span><span id="how_to_enable_key_scenarios"></span><span id="HOW_TO_ENABLE_KEY_SCENARIOS"></span>如何启用关键方案


使用下列准则来帮助你启用这些关键方案。

### <a name="span-idenablesimpspanspan-idenablesimpspanenable-a-simple-connect-experience"></a><span id="enablesimp"></span><span id="ENABLESIMP"></span>启用简单连接体验

必须提供要包含在 Windows 8、Windows 8.1 或 Windows 10 APN 数据库中的最小数据量。 有关 Windows APN 数据库的详细信息，请参阅 [APN 数据库概述](apn-database-overview.md)。

您必须提供以下信息以包括在 APN 数据库中：

-   要使 Windows 无需用户输入 APN 或访问字符串即可连接到移动宽带网络，必须提供 APNs 和/或访问字符串。

-   要使 Windows 在未检测到 Internet 连接时自动打开移动宽带网站，你必须提供网站的 URL。

### <a name="span-iddetectspanspan-iddetectspandetect-internet-access"></a><span id="detect"></span><span id="DETECT"></span>检测 Internet 访问

当 Windows 首次连接到网络以确定 Internet 连接时，它会执行各种网络测试。 这些测试的目标站点是 `www.msftconnecttest.com` ，它是专用于连接测试的保留域。

若要避免误报或假负，你的网络必须 `www.msftconnecttest.com` 仅在用户具有常规 Internet 访问权限时才允许访问。 没有活动数据计划连接到网络的用户无权访问 `www.msftconnecttest.com` 。 有关详细信息，请参阅 [当计算机连接到公司网络或公用网络时，会打开 Internet Explorer 或 Edge 窗口](https://support.microsoft.com/en-us/help/4494446/an-internet-explorer-or-edge-window-opens-when-your-computer-connects)。

### <a name="span-idwebaccessspanspan-idwebaccessspanweb-site-access"></a><span id="webaccess"></span><span id="WEBACCESS"></span>网站访问

移动运营商通常使用以下两种方法之一限制没有活动数据计划的用户的网络访问权限：

-   将用户保留在相同的 APN 上，但阻止对所有网络目标的访问，但计划购买和激活所需的最少服务器集除外。 此实现也称为 "围墙园"。

-   将用户切换到永不提供 Internet 访问的购买 APN，但允许访问计划购买和激活所需的服务器集。

没有活动数据计划的用户必须能够通过使用其中一种方法访问移动宽带网站。 此外，用户必须能够通过 Internet 使用 HTTPS 连接访问网站。

### <a name="span-iddevinfspanspan-iddevinfspandevice-information"></a><span id="devinf"></span><span id="DEVINF"></span>设备信息

当 Windows 使用移动运营商的 URL 从 APN 数据库) 的 [operator](operator.md) 元素中 (AccountExperienceURL 属性时，windows 将提供完成移动宽带网站激活所需的设备信息。 此设备信息将作为 HTTPS 请求的参数传递到网站。

Url 的格式为 **https://Operator url \[ ？ propN = valN \[&\] \* \] propN = valN**，其中：

-   **操作员 URL** 你的 URL，并将其存储在 APN 数据库中

-   **propN** 属性名称。

-   **valN** 对应于 "值名称" 的值。

下表列出了可以包含的属性。 如果移动宽带设备未提供属性值，则不会包括该属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>属性值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SubId</p></td>
<td><p>订户 ID</p>
<ul>
<li><p>对于 GSM 设备： IMSI 最多 (15 位) </p></li>
<li><p>对于 CDMA 设备：) 的最小或最小 (IRM (10 位数) </p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DevId</p></td>
<td><p>设备 ID</p>
<ul>
<li><p>对于 GSM 设备： IMEI (最多15位) </p></li>
<li><p>对于 CDMA 设备： ESN (11 位数) 或 MEID (17 位) </p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IccId</p></td>
<td><p>SIM ICCID (19-20 位数) </p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idconfigure_the_computerspanspan-idconfigure_the_computerspanspan-idconfigure_the_computerspanconfigure-the-computer"></a><span id="Configure_the_computer"></span><span id="configure_the_computer"></span><span id="CONFIGURE_THE_COMPUTER"></span>配置计算机

用户购买数据计划或通过使用网站激活移动宽带设备后，对计算机进行以下配置更改可能会很有用：

-   定义移动宽带连接配置文件

-   提供帐户数据

-   定义 Wi-Fi 热点连接配置文件

-   指示计算机重新连接移动宽带设备

移动宽带网站还可以应用可通过使用移动宽带应用来应用于计算机的相同帐户设置元数据。 在网页的 JavaScript 中，检查 [**msProvisionNetworks**](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) 方法的可用性。 如果存在，浏览器可以将帐户预配元数据传输到 Windows。

有关帐户预配元数据的详细信息，请参阅 [帐户预配](account-provisioning.md)。

**注意**  
在网站提供时，必须使用扩展验证 (EV) 证书对帐户预配元数据进行签名。

 

 

