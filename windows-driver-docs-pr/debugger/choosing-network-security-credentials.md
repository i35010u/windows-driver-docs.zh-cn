---
title: 选择网络安全凭据
description: 选择网络安全凭据
keywords:
- SymProxy，网络安全
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f59c51a4ef9831fa338e4b631f83848cb9b6c104
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826719"
---
# <a name="choosing-network-security-credentials"></a>选择网络安全凭据


符号代理服务器必须从具有相应权限的安全上下文中运行，以便访问你计划使用的符号存储区。 如果从外部 Web 存储（如）获取符号 https://msdl.microsoft.com/download/symbols ，则符号代理服务器必须从任何防火墙外部访问 Web。 如果你从网络中的其他计算机获取文件，则符号代理服务器必须具有从这些位置读取文件的适当权限。 两种可能的选择是将符号代理服务器设置为作为 **网络服务** 帐户进行身份验证，或者创建在 Active Directory 域服务和其他用户帐户一起管理的用户帐户。

**注意**   最佳做法是将此帐户的特权限制为只需读取文件并将其复制到 c： \\ symstore。 此限制可防止访问你的 HTTP 存储的客户端损坏系统。

 

**注意**  请确保此处提供的选项在你的环境中有意义。 不同的组织具有不同的安全需求和要求。 修改此处所述的过程以支持组织的安全要求。

 

### <a name="span-idauthenticate_as_a_network_servicespanspan-idauthenticate_as_a_network_servicespanauthenticate-as-a-network-service"></a><span id="authenticate_as_a_network_service"></span><span id="AUTHENTICATE_AS_A_NETWORK_SERVICE"></span>作为网络服务进行身份验证

**网络服务** 帐户内置于 Windows，因此没有额外的步骤来创建新帐户。 在此示例中，我们将在名为 *corp* 的域上 *SymMachineName* 配置符号代理服务器的计算机命名为。

必须将外部符号存储或 Internet 代理配置为允许此计算机的 **网络服务** 帐户 (计算机帐户) 才能成功进行身份验证。 可通过两种方式实现此目的：

-   允许访问外部存储或 Internet 代理上 **经过身份验证的用户** 组。

-   允许访问计算机帐户 *corp \\ SymMachineName $*。 此选项更安全，因为它将访问权限限制为仅限符号代理服务器的 "网络服务" 帐户。

### <a name="span-idauthenticate_as_a_domain_userspanspan-idauthenticate_as_a_domain_userspanspan-idauthenticate_as_a_domain_userspanauthenticate-as-a-domain-user"></a><span id="Authenticate_as_a_Domain_User"></span><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>作为域用户进行身份验证

在此示例中，我们假设用户帐户名为 " *corp*" 的域上的 " *SymProxyUser* "。

**将用户帐户添加到 IIS \_ USRS 组**

1.  从 " **管理工具** " 中打开 " **计算机管理**"。

2.  展开“本地用户和组”。

3.  单击“组”。

4.  双击中间窗格中的 " **IIS \_ USRS** "，然后选择 " **属性**"。

5.  在 " **成员** " 部分中，单击 " **添加**"。

6.  在标有 "**输入要选择的对象名称**" 窗格中键入 *corp \\ SymProxyUser* 。

7.  若要退出 " **选择用户、计算机或组** " 对话框，请单击 **"确定"**。

8.  若要退出 **IIS \_ USRS 属性**，请单击 **"确定"**。

9.  关闭 " **计算机管理** " 控制台。

**设置 IIS 以使用帐户**

1.  从 " **管理工具** " **Internet Information Services (IIS) 管理器** 打开。

2.  展开 **"网站"**。

3.  右键单击 " **默认** 网站"，然后选择 " **属性**"。

4.  单击“目录安全性”选项卡。

5.  在 " **身份验证和访问控制** " 部分中，单击 " **编辑 ...**"。

6.  请确保已选中 " *启用匿名访问* "。

7.  输入有权访问远程符号服务器存储的帐户的凭据 (s)  ( "corp \\ SymProxyUser" ) ，然后单击 **"确定**"。

8.  询问时重新输入密码，然后单击 **"确定"**。

9.  若要退出 **默认网站属性**，请单击 **"确定"**。

10. 可能会出现 " *继承覆盖* " 对话框。 如果是这样，请选择要将其应用到的虚拟目录。

### <a name="span-idauthenticate_as_a_domain_userspanspan-idauthenticate_as_a_domain_userspanauthenticate-as-a-domain-user-using-the-iis_wpg-group"></a><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>使用 IIS WPG 组作为域用户进行身份验证 \_

在此示例中，名为 *corp* 的域上的用户帐户名为 *SymProxyUser* 。 若要对此用户帐户进行身份验证，必须将其添加到 **IIS \_ WPG** 组。

**将用户帐户添加到 IIS \_ WPG 组**

1.  从 " **管理工具** " 中打开 " **计算机管理**"。

2.  展开“本地用户和组”。

3.  单击“组”。

4.  双击右侧窗格中的 " **IIS \_ WPG** "。

5.  单击“添加”  。

6.  在标有 "**输入要选择的对象名称**" 窗格中键入 *corp \\ SymProxyUser* 。

7.  若要退出 " **选择用户、计算机或组** " 对话框，请单击 **"确定"**。

8.  若要退出 **IIS \_ WPG 属性**，请单击 **"确定"**。

9.  关闭 " **计算机管理** " 控制台。

 

 





