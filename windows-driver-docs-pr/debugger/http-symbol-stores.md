---
title: HTTP 符号存储
description: HTTP 符号存储
keywords:
- HTTP 符号存储区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 735b2dacf351b401cdf0c7021b10e9e16b97e332
ms.sourcegitcommit: 119a8f0435127a41cd215063200f67cd6eb51ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218277"
---
# <a name="http-symbol-stores"></a>HTTP 符号存储


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


通过使用通过调试器) 附带的 symsrv.dll (支持的 SRV 协议，可以使用 HTTP (而不只是 UNC/SMB) 访问符号存储区。

当防火墙不允许客户端与服务器之间的 SMB 时，通常使用 HTTP 而不是 SMB。 生产环境和实验室环境就是这种情况的一个很好的例子。

HTTP 符号服务器不能是符号路径链中的下游存储，因为它是只读的。  (ISAPI 筛选器的符号服务器代理) 绕过此限制。 SymProxy 使用预配置的上游符号存储将缺少的文件下载到服务器的文件系统。 该筛选器将文件下载到文件系统，从而允许 IIS 将文件下载到客户端，从而还原符号存储区链接的概念。 有关详细信息，请参阅 [SymProxy](symproxy.md) 。

将 IIS 配置为符号存储相对容易，因为符号文件只作为静态文件提供。 唯一的非默认设置是 MIME 类型的配置，以允许将符号文件作为二进制流下载。 为此，可以使用 \* 应用于符号文件夹的虚拟目录的 "" 通配符。

为了使符号存储区可通过 Internet 访问，必须同时配置包含符号文件和 Internet Information Services (IIS) 的目录。

**注意**  由于将 IIS 配置为提供符号文件的方式，不建议将同一服务器实例用于任何其他目的。 通常，符号服务器所需的安全设置对于其他用途（例如面向外部的商业服务器）将毫无意义。 请确保此处所述的示例配置适用于你的环境，并根据你的具体需要对其进行调整。

 

### <a name="span-idconfiguring_the_directoriesspanspan-idconfiguring_the_directoriesspancreating-the-symbol-directory"></a><span id="configuring_the_directories"></span><span id="CONFIGURING_THE_DIRECTORIES"></span>创建符号目录

首先选择将用作符号存储区的目录。 在我们的示例中，我们调用此目录 c： \\ symstore，并且网络上的服务器名称为 \\ SymMachineName。

有关如何填充符号存储区的详细信息，请参阅 [SymStore](symstore.md) 和 [符号存储文件夹树](symbol-store-folder-tree.md)。

### <a name="span-idconfiguring_iisspanspan-idconfiguring_iisspanconfiguring-iis"></a><span id="configuring_iis"></span><span id="CONFIGURING_IIS"></span>配置 IIS

必须通过创建虚拟目录和配置 MIME 类型，将 (IIS) Internet Information Services 配置为提供符号。 完成此操作后，可以选择身份验证方法。

**创建虚拟目录**

1.  打开“Internet Information Services (IIS)管理器” 。

2.  导航到 **"网站"。**

3.  右键单击 " **默认** 网站" 或要使用的网站的名称，然后选择 " **添加虚拟目录 ...**"。

4.  键入 **别名** 的 **符号**，然后单击 "**下一步**"。

    为了便于管理，建议将同一名称用于文件夹、共享和虚拟目录。

5.  对于 " **路径** "，请输入 **c： \\ SymStore** ，然后单击 " **下一步**"。

6.  单击 **"确定"** 以完成添加虚拟目录的操作。

为服务器执行一次子目录配置过程。 请注意，这是全局设置，它会影响未托管在站点的根文件夹中的应用程序。

**子目录配置**

1.  导航到 " **\[ 计算机 \]**"。

2.  打开 **配置编辑器**。

3.  导航到 " **系统 ApplicationHost/站点**"。

4.  展开 **virtualDirectoryDefaults**。

5.  将 **了 allowsubdirconfig** 设置为 *False*。

为服务器执行此过程一次。 请注意，这是全局设置，它会影响未托管在站点的根文件夹中的应用程序。

**Optionaly 使符号文件可浏览**

1.  导航到 **\[ 计算机 \] |站点 |\[网站 \] |符号**。

2.  双击中间窗格中的 " **目录浏览** "。

3.  单击右窗格中的 " **启用** "。

下载内容的 MIME 类型需要设置为 application/八进制流，以允许 IIS 传递所有符号文件。

**配置 MIME 类型**

1. 右键单击 **符号** 虚拟目录，然后选择 " **属性**"。

2. 选择 " **HTTP 标头**"。

3. 单击 " **MIME 类型**"。

4. 单击 **“新建”** 。

5. 对于 " **扩展**"，键入 **\*** 。

6. 对于 **MIME 类型**，键入 **application/八进制流**。

7. 若要退出 " **MIME 类型** " 对话框，请单击 **"确定"**。

8. 若要退出 **符号属性**，请单击 **"确定"**。

可以编辑 web.config 文件，以配置符号的 MIME 类型。 此方法会清除继承的 MIME 类型，并添加 "全部捕获" 通配符 \* MIME 类型。 当在某些 IIS 配置中继承 MIME 类型时，可能需要此方法。

**使用 web.config 配置 MIME 类型**

1.  编辑 web.config 文件，如下所示。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <system.webServer>
            <directoryBrowse enabled="true" />
            <staticContent>
                <clear />
                <mimeMap fileExtension=".*" 
    mimeType="application/octet-stream" />
            </staticContent>
        </system.webServer>
    </configuration>
    ```

2.  重启 IIS。

IIS 现在可以为符号存储区中的所有类型的符号文件提供服务。

## <a name="span-idconfiguring_authenticationspanspan-idconfiguring_authenticationspanspan-idconfiguring_authenticationspanconfiguring-authentication"></a><span id="Configuring_Authentication"></span><span id="configuring_authentication"></span><span id="CONFIGURING_AUTHENTICATION"></span>配置身份验证


可以将 IIS 配置为使用 "集成 Windows 身份验证"，以便 (windbg.exe 例如) 的客户端可以针对 IIS 自动进行身份验证，而不会提示最终用户提供凭据。

**注意**  仅在 IIS 上配置 Windows 身份验证，以控制对符号服务器的访问（如果该权限适用于你的环境）。 如果你的环境需要，还可以使用其他安全选项来进一步控制对 IIS 的访问。

 

**将身份验证方法配置为匿名**

1.  **(IIS) 管理器启动 Internet Information Services**。

2.  导航到 **\[ 计算机 \] |站点 |\[网站 \] |符号**。

3.  双击中间窗格中的 " **身份验证** "。

4.  在 " **身份验证和访问控制** " 下，单击 " **编辑**"。

5.  右键单击 " **Windows 身份验证** "，然后选择 " **启用**"。

6.  对于所有其他身份验证提供程序，请右键单击每个提供程序，然后选择 " **禁用**"。

7.  单击 **"确定"** 完成身份验证配置。

如果未列出 "窗口身份验证"，请使用 **"打开和关闭 Windows 功能** " 来启用此功能。 此功能在每个版本的 Windows 中的位置不同。 在 Windows 8.1/Windows 2012 R2 中，它位于 Internet Information Services |World Wide Web 服务 |安全.

## <a name="span-iddisable_kerberos_supportspanspan-iddisable_kerberos_supportspanspan-iddisable_kerberos_supportspandisable-kerberos-support"></a><span id="Disable_Kerberos_Support"></span><span id="disable_kerberos_support"></span><span id="DISABLE_KERBEROS_SUPPORT"></span>禁用 Kerberos 支持


SymSrv.dll 在连接到 IIS 时不支持 Kerberos 身份验证。 因此，必须在 IIS 中禁用 Kerberos 身份验证，并且 NTLM 需要设置为唯一的 Windows 身份验证协议。

**注意**  仅在适用于你的环境时禁用 Kerberos 安全性。

 

**使用 appcmd.exe禁用 Kerberos 支持**

1.  打开“命令提示符”窗口

2.  若要禁用 Kerberos 并强制使用 NTLM，请使用此命令：

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='NTLM']" /commit:apphost
    ```

3.  若要返回启用了 Kerberos 的默认值，请使用此命令：

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='Negotiate,NTLM']" /commit:apphost
    ```

## <a name="span-idconfiguring_symsrv_client_authentication_promptsspanspan-idconfiguring_symsrv_client_authentication_promptsspanspan-idconfiguring_symsrv_client_authentication_promptsspanconfiguring-symsrv-client-authentication-prompts"></a><span id="Configuring_SymSrv_Client_Authentication_Prompts"></span><span id="configuring_symsrv_client_authentication_prompts"></span><span id="CONFIGURING_SYMSRV_CLIENT_AUTHENTICATION_PROMPTS"></span>配置 SymSrv 客户端身份验证提示


当 SymSrv 接收到身份验证请求时，调试器可以显示 "身份验证" 对话框，或根据配置方式自动拒绝请求。 你可以使用 | off 上的！符号提示符来配置此行为。 例如，若要打开提示，请使用此命令。

```dbgcmd
!sym prompts on
```

若要检查当前设置，请使用此命令。

```dbgcmd
!sym prompts
```

有关详细信息，请参阅 [**！符号**](-sym.md) 和 [防火墙和代理服务器](firewalls-and-proxy-servers.md)。

 

 





