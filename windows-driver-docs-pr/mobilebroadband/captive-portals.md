---
title: 强制网络门户
description: 强制网络门户
ms.assetid: 6f710440-3012-4bf4-92cc-3743b0f4fd34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c117d4da083567f93289d40a2b5be69f3cf9973e
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304298"
---
# <a name="captive-portals"></a>强制网络门户


大多数热点都通过使用捕获门户来实现客户交互，该门户是一个受限的网络连接，其中的所有客户端 HTTP 请求都将重定向到提供商的网站。 然后，网站可以提示用户同意操作员的条款和条件，输入付款信息，或输入凭据以验证先前的付款方式。

使用此类体验存在几个问题：

-   其他应用程序 (例如，电子邮件客户端) 也会重定向。 如果用户首先尝试使用 web 浏览器以外的其他应用程序，他们将会在不知道如何解决错误的情况下遇到错误。

-   如果尝试通过安全套接字层 (SSL) 进行初始连接，则在用户重定向到捕获门户之前，浏览器会向用户显示一条安全警告。 这会给用户带来混乱的体验，因为用户必须忽略安全警告才能进行连接。

如果检测到了捕获的门户，windows 8、Windows 8.1 和 Windows 10 支持通过立即打开 web 浏览器来捕获门户网络。 用户会在其设备的前景看到你的品牌网页，这有助于用户了解通过使用该门户进行身份验证时应采取的操作。

Windows 提供了一些机制，使用户可以在后续连接尝试时绕过这些门户。 但是，通常情况下，捕获的门户始终是首次使用的用户所遇到的体验。

本主题讨论使用 "捕获门户" 的以下最佳做法：

-   [一致的连接处理](#cch)

-   [触摸友好网页](#touchfr)

-   [购买后预配](#pap)

-   [提供应用安装](#appinst)

## <a name="span-idcchspanspan-idcchspanconsistent-connection-handling"></a><span id="cch"></span><span id="CCH"></span>一致的连接处理


若要在客户端首次连接到网络时确定 Internet 连接和保持门户状态，Windows 将执行一系列网络测试。 这些测试的目标站点是 **msftncsi.com**，它是专用于连接测试的保留域。 检测到捕获的门户后，这些测试会定期重复进行，直到释放了捕获的门户。

若要避免误报或误报测试结果，你的捕获门户不应执行以下操作：

- 当用户无权访问 Internet 时，允许访问 <strong>www.msftncsi.com</strong> 。

- 更改显示给客户端的 "捕获" 门户行为。 例如，不要重定向一些请求并删除其他请求;应该继续重定向所有请求，直到身份验证成功。

  **注意**  
  拒绝服务缓解应该基于每个客户端的尝试频率，而不是基于每个客户端的尝试次数或来自所有客户端的总尝试次数。

     

## <a name="span-idtouchfrspanspan-idtouchfrspantouch-friendly-web-pages"></a><span id="touchfr"></span><span id="TOUCHFR"></span>触摸友好网页


Windows 8、Windows 8.1 和 Windows 10 体验旨在首先接触。 这将扩展到网页。 考虑为触摸用户提供具有更大、易于控制的控件的网页布局。 如果需要，请使用不需要过多滚动即可与之进行交互的布局，并将流分解到多个页面。 有关触控友好 web 设计的详细信息，请参阅 [设计触控输入](https://msdn.microsoft.com/library/windows/apps/hh465415.aspx)。

## <a name="span-idpapspanspan-idpapspanprovision-after-purchase"></a><span id="pap"></span><span id="PAP"></span>购买后预配


可应用于应用的同一预配文件也可由网站应用。 在网页的 JavaScript 中，检查 [**msProvisionNetworks**](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) 方法的可用性。 如果存在，浏览器可以将设置文件中继到操作系统。 有关如何生成此设置文件的详细信息，请参阅 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md) 。

**注意**   此设置文件在网站或不是移动宽带应用程序提供的应用程序提供时必须进行签名。

 

通过传递 XML 预配文件，操作系统可以自动连接到用户服务中包含的其他网络，即使它们具有不同的服务集标识符 (Ssid) 。 如果使用静态无线 Internet 服务提供商漫游 (WISPr) 凭据，它还可实现更流畅的连接体验，因为在将来，Windows 可以使用这些凭据自动进行身份验证。

## <a name="span-idappinstspanspan-idappinstspanoffer-app-installation"></a><span id="appinst"></span><span id="APPINST"></span>提供应用安装


Windows 8、Windows 8.1 和 Windows 10 的最丰富的体验是通过使用移动宽带应用程序实现的。 不可能只允许通过捕获的门户访问 Microsoft Store 中的一个应用，因此在用户获取 Internet 连接之前无法安装该应用。 但是，用户经过身份验证后，请考虑将它们定向到 Microsoft Store 以安装移动宽带应用。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证方法](integrating-windows-with-wireless-hotspots.md)

 

