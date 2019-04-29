---
title: 选择网络安全凭据
description: 选择网络安全凭据
ms.assetid: f53bda2b-a5e7-4a8e-ac31-44c92f306b7a
keywords:
- SymProxy，网络安全
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f754585f5b4b561d83cbb36d2bc2cc73b6f9730c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375103"
---
# <a name="choosing-network-security-credentials"></a>选择网络安全凭据


符号代理服务器必须运行从安全上下文与适当的特权访问到你打算使用符号存储区。 如果如获取符号从外部 Web 存储 https://msdl.microsoft.com/download/symbols，符号代理服务器必须访问之外的任何防火墙从 Web。 如果你获取文件的其他计算机在网络上，符号代理服务器必须具有从这些位置读取文件的相应权限。 两个可能的选项是设置符号代理服务器进行身份验证作为**网络服务**帐户，或创建的用户帐户，托管在 Active Directory 域服务以及其他用户帐户。

**请注意**  建议限制为仅需读取文件并将其复制到 c： 此帐户的特权\\symstore。 此限制可以防止损坏系统访问 HTTP 存储区的客户端。

 

**请注意**  请确保此处显示的选项在环境中进行有意义。 不同的组织具有不同的安全需求和要求。 修改此处所述来支持你的组织的安全要求的过程。

 

### <a name="span-idauthenticateasanetworkservicespanspan-idauthenticateasanetworkservicespanauthenticate-as-a-network-service"></a><span id="authenticate_as_a_network_service"></span><span id="AUTHENTICATE_AS_A_NETWORK_SERVICE"></span>作为网络服务进行身份验证

**网络服务**帐户内置于 Windows，因此没有任何额外的步骤来创建新的帐户。 对于此示例中，我们命名为正在配置符号代理服务器的计算机*SymMachineName*上名为的域*corp*。

必须配置为允许此计算机的外部符号存储区或 Internet 代理服务器**网络服务**帐户 （计算机帐户），若要成功进行身份验证。 有两种方法来实现此目的：

-   允许访问**Authenticated Users**组在外部存储区或 Internet 代理上。

-   允许计算机帐户的访问权限*corp\\SymMachineName$*。 此选项是更安全，因为它限制只是符号代理服务器的"网络服务"帐户的访问权限。

### <a name="span-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanauthenticate-as-a-domain-user"></a><span id="Authenticate_as_a_Domain_User"></span><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>以域用户的身份验证

对于此示例中，我们将假定名为的用户帐户*SymProxyUser*上一个名为域*corp*。

**若要将用户帐户添加到 IIS\_USRS 组**

1.  从**管理工具**打开**计算机管理**。

2.  展开**本地用户和组**。

3.  单击“组” 。

4.  双击**IIS\_USRS**在中心窗格中，选择**属性**。

5.  下**成员**部分中，单击**添加**。

6.  类型*corp\\SymProxyUser*中的标记为窗格**输入要选择的对象名称**。

7.  若要退出**选择用户、 计算机或组**对话框中，单击**确定**。

8.  若要退出**IIS\_USRS 属性**，单击**确定**。

9.  关闭**计算机管理**控制台。

**IIS 设置为使用的帐户**

1.  从**管理工具**打开**Internet Information Services (IIS) Manager**。

2.  展开**网站**。

3.  右键单击**Default Web Site** ，然后选择**属性**。

4.  单击**目录安全性**选项卡。

5.  在中**身份验证和访问控制**部分中，单击**编辑...**.

6.  请确保*启用匿名访问*检查。

7.  输入有权访问远程符号服务器存储的帐户的凭据 ("corp\\SymProxyUser")，然后单击**确定**。

8.  重新输入密码时要求，然后单击**确定**。

9.  若要退出**默认网站属性**，单击**确定**。

10. 您可能会出现*继承覆盖*对话框。 如果是这样，选择你想要有此哪些虚拟目录适用于。

### <a name="span-idauthenticateasadomainuserspanspan-idauthenticateasadomainuserspanauthenticate-as-a-domain-user-using-the-iiswpg-group"></a><span id="authenticate_as_a_domain_user"></span><span id="AUTHENTICATE_AS_A_DOMAIN_USER"></span>以域用户使用 IIS 的身份验证\_WPG 组

对于此示例中，名为的用户帐户*SymProxyUser*上名为的域*corp*。 要对此用户帐户进行身份验证，必须将其添加到**IIS\_WPG**组。

**若要将用户帐户添加到 IIS\_WPG 组**

1.  从**管理工具**打开**计算机管理**。

2.  展开**本地用户和组**。

3.  单击“组” 。

4.  双击**IIS\_WPG**右窗格中。

5.  单击**添加**。

6.  类型*corp\\SymProxyUser*中的标记为窗格**输入要选择的对象名称**。

7.  若要退出**选择用户、 计算机或组**对话框中，单击**确定**。

8.  若要退出**IIS\_WPG 属性**，单击**确定**。

9.  关闭**计算机管理**控制台。

 

 





