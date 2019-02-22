---
title: 强制门户网站
description: 强制门户网站
ms.assetid: 6f710440-3012-4bf4-92cc-3743b0f4fd34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a014465c600787e2c878dd17a3c572607a338128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541171"
---
# <a name="captive-portals"></a>强制门户网站


大多数热点实现客户交互使用强制网络门户，它是在其中的所有客户端 HTTP 请求将重定向到提供商的网站的受限的网络连接。 然后操作员的条款和条件，即表示同意，提示用户输入付款信息，或输入凭据以验证之前支付排列方式，可以 web 站点。

通过使用这种体验存在几个问题：

-   其他应用程序 （如电子邮件客户端） 也将重定向。 如果用户先尝试使用 web 浏览器以外的应用，它们将不知道如何解决这些问题会遇到错误。

-   如果通过安全套接字层 (SSL) 建立初始连接尝试，在浏览器安全警告向用户显示之前用户重定向到强制网络门户。 这将创建令人困惑的用户体验，因为它们必须忽略安全警告，若要获取连接。

Windows 8、 Windows 8.1 和 Windows 10 通过立即打开 web 浏览器，如果检测到强制网络门户支持强制网络门户网络。 用户将看到经过品牌打造的网页中的设备，这有助于他们了解为了使用强制网络门户进行身份验证，而应采取哪些操作前景色。

Windows 提供了可以让用户绕过强制门户网站上的后续连接尝试的机制。 但是，强制网络门户始终是遇到的第一次用户的体验。

本主题讨论使用强制门户网站的以下最佳实践：

-   [一致的连接处理](#cch)

-   [触摸式网页](#touchfr)

-   [购买后预配](#pap)

-   [产品/服务的应用安装](#appinst)

## <a name="span-idcchspanspan-idcchspanconsistent-connection-handling"></a><span id="cch"></span><span id="CCH"></span>一致的连接处理


若要确定 Internet 连接和强制网络门户状态，当客户端首次连接到网络，Windows 将执行一系列的网络测试。 这些测试的目标站点是**msftncsi.com**，这是专门用于连接测试保留的域。 检测到强制网络门户时，直到释放强制网络门户定期重复执行这些测试。

若要避免错误的正或假负测试结果，强制网络门户应执行以下操作：

- 允许访问<strong>www.msftncsi.com</strong>用户不具有 Internet 访问权限。

- 更改显示给客户端强制网络门户行为。 例如，不将一些请求重定向并删除其他请求;应继续将所有请求重都定向，直到成功进行身份验证。

  **注意**  
  拒绝服务的缓解措施应基于每个客户端、 不尝试每个客户端数或总尝试从所有客户端尝试的频率。

     

## <a name="span-idtouchfrspanspan-idtouchfrspantouch-friendly-web-pages"></a><span id="touchfr"></span><span id="TOUCHFR"></span>触摸式网页


Windows 8、 Windows 8.1 和 Windows 10 体验专为触摸优先。 这将扩展的 web 页面。 请考虑对 web 页与触控用户更大、 易于目标控件进行布局。 使用，不需要过多的滚动，若要与之交互，如有必要将流分为多个页面的布局。 触摸式 web 设计的详细信息，请参阅[设计的触摸输入](https://msdn.microsoft.com/library/windows/apps/hh465415.aspx)。

## <a name="span-idpapspanspan-idpapspanprovision-after-purchase"></a><span id="pap"></span><span id="PAP"></span>购买后预配


此外可以通过网站应用同一应用程序，可以应用的预配文件。 在 web 页面的 JavaScript 中，检查的可用性[ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/dn529170)方法。 如果存在，在浏览器可以将中继到操作系统的预配文件。 请参阅[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)有关如何生成此配置文件的详细信息。

**请注意**  时由网站或不是移动宽带应用的应用提供此配置文件必须进行签名。

 

传递 XML 置备文件使操作系统以自动连接到用户的服务中包含其他网络，即使它们具有不同的服务设置标识符 (Ssid)。 如果使用静态无线 Internet 服务提供商漫游 (WISPr) 凭据，但它还启用了更流畅的连接体验，因为在将来，Windows 可以自动进行身份验证使用这些凭据。

## <a name="span-idappinstspanspan-idappinstspanoffer-app-installation"></a><span id="appinst"></span><span id="APPINST"></span>产品/服务的应用安装


Windows 8、 Windows 8.1 和 Windows 10 的最丰富的体验是使用移动宽带应用。 不能允许对强制网络门户中，通过 Microsoft Store 中只有一个应用的访问，因此不能在用户获取 Internet 连接之前安装该应用。 但是，用户进行身份验证后，请考虑将它们定向到 Microsoft Store 安装你的移动宽带应用。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[热点身份验证方法](hotspot-authentication-methods.md)

 

 






