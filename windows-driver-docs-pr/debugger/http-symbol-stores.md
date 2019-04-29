---
title: HTTP 符号存储
description: HTTP 符号存储
ms.assetid: b7dd1f3c-0135-4b69-9d70-b7cbf37fa969
keywords:
- HTTP 符号存储区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b439221eabe7addb4a0221a2ac010d219631bb89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379143"
---
# <a name="http-symbol-stores"></a>HTTP 符号存储


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


通过使用 SRV 协议通过 symsrv.dll （附带调试程序） 支持，可使用 HTTP （而不是只是 UNC/SMB) 访问符号存储区。

当防火墙不允许 SMB 客户端和服务器之间，而不是 SMB 通常使用 HTTP。 生产和实验室环境是很好的此示例。

HTTP 符号服务器不能为符号路径链由于其只读特性中的下游存储。 符号服务器代理 （ISAPI 筛选器） 突破了此限制。 SymProxy 将缺少的文件下载到服务器的文件系统使用预配置的上游符号存储区。 筛选器将文件下载到文件系统，从而允许 IIS 以将文件下载到客户端，从而还原符号存储区链接的概念。 请参阅[SymProxy](symproxy.md)有关详细信息。

将 IIS 配置为符号存储区就像文件只是用作静态文件的符号相对较容易。 仅非默认设置为允许下载二进制流的形式的符号文件的 MIME 类型配置。 这可以通过使用"\*"应用到的虚拟目录的符号文件夹的通配符。

为使存储的符号通过 Internet 访问，必须配置包含的符号文件和 Internet 信息服务 (IIS) 的这两个目录。

**请注意**  由于 IIS 将配置为提供符号文件的方式，建议不要在同一服务器实例，用于任何其他用途。 通常的符号服务器的所需的安全设置将毫无意义用于其他用途，例如外部的面向公众 commerce server。 请确保此处所述的示例配置适合您的环境并根据你的特定需求对其进行调整。

 

### <a name="span-idconfiguringthedirectoriesspanspan-idconfiguringthedirectoriesspancreating-the-symbol-directory"></a><span id="configuring_the_directories"></span><span id="CONFIGURING_THE_DIRECTORIES"></span>创建符号目录

选择将用作符号存储区的目录开始。 在示例中，我们调用此目录 c:\\symstore 和在网络上的服务器的名称是\\SymMachineName。

有关如何填充符号存储区的详细信息，请参阅[SymStore](symstore.md)并[符号存储文件夹树](symbol-store-folder-tree.md)。

### <a name="span-idconfiguringiisspanspan-idconfiguringiisspanconfiguring-iis"></a><span id="configuring_iis"></span><span id="CONFIGURING_IIS"></span>配置 IIS

必须配置 Internet 信息服务 (IIS) 为通过创建虚拟目录和配置 MIME 类型提供符号。 这样做后，可以选择的身份验证方法。

**若要创建虚拟目录**

1.  从**管理工具**打开**Internet Information Services (IIS) Manager**。

2.  导航到**网站**。

3.  右键单击**Default Web Site**或正在使用的站点的名称，然后选择**添加虚拟目录...**.

4.  类型**符号**有关**别名**然后单击**下一步**。

    为便于管理，建议相同的名称，用于文件夹、 共享和虚拟目录。

5.  有关**路径**输入**c:\\SymStore**然后单击**下一步**。

6.  单击**确定**以完成添加虚拟目录。

执行一次服务器子目录配置过程。 请注意这是一种全局设置，将影响未托管站点的根文件夹中的应用程序。

**子目录配置**

1.  导航到**\[计算机\]**。

2.  打开**配置编辑器**。

3.  导航到**ApplicationHost/站点系统**。

4.  展开**virtualDirectoryDefaults**。

5.  设置**allowSubDirConfig**到*False*。

服务器一次执行此过程。 请注意这是一种全局设置，将影响未托管站点的根文件夹中的应用程序。

**选择性地使符号文件可浏览**

1.  导航到**\[计算机\]|站点 |\[网站\]|符号**。

2.  双击**目录浏览**的中心窗格中。

3.  单击**启用**右窗格中。

下载的内容的 MIME 类型应设置为应用程序/八进制流，以允许由 IIS 提供所有符号文件。

**配置 MIME 类型**

1. 右键单击**符号**虚拟目录，然后选择**属性**。

2. 选择**HTTP 标头**。

3. 单击**MIME 类型**。

4. 单击**新建**。

5. 有关**扩展**，键入 * *\\* * *。

6. 有关**MIME 类型**，类型**应用程序/八进制流**。

7. 若要退出**MIME 类型**对话框中，单击**确定**。

8. 若要退出**符号属性**，单击**确定**。

可以编辑 web.config 文件以配置 MIME 类型的符号。 此方法将清除继承的 MIME 类型，并将添加全方位的通配符\*MIME 类型。 MIME 类型继承而来在某些 IIS 配置时，这种方法可能有必要。

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

2.  重新启动 IIS。

IIS 现在已准备好提供符号存储区中的所有类型的符号文件。

## <a name="span-idconfiguringauthenticationspanspan-idconfiguringauthenticationspanspan-idconfiguringauthenticationspanconfiguring-authentication"></a><span id="Configuring_Authentication"></span><span id="configuring_authentication"></span><span id="CONFIGURING_AUTHENTICATION"></span>配置身份验证


就可以将 IIS 配置为使用"集成 Windows 身份验证"，以便客户端 (例如 windbg.exe) 可以自动进行身份验证对 IIS 而不会提示最终用户的凭据。

**请注意**  仅控制到符号服务器的访问，如果这是适用于你的环境在 IIS 上配置 Windows 身份验证。 如果这是环境的需要，则 IIS 到其他安全选项可用于进一步控制访问。

 

**以匿名方式配置身份验证方法**

1.  启动**Internet Information Services (IIS) 管理器**。

2.  导航到**\[计算机\]|站点 |\[网站\]|符号**。

3.  双击**身份验证**的中心窗格中。

4.  下**身份验证和访问控制**单击**编辑**。

5.  右键单击**Windows 身份验证**，然后选择**启用**。

6.  对于所有其他身份验证提供程序，右键单击每个提供程序，然后选择**禁用**。

7.  单击**确定**完成配置身份验证。

如果未列出 Window 身份验证，请使用**打开或关闭打开的 Windows 功能**以启用该功能。 在每个版本的 Windows 中不同的功能的位置。 在 Windows 8.1 / Windows 2012 R2，它位于 Internet 信息服务 |World Wide Web 服务 |安全性。

## <a name="span-iddisablekerberossupportspanspan-iddisablekerberossupportspanspan-iddisablekerberossupportspandisable-kerberos-support"></a><span id="Disable_Kerberos_Support"></span><span id="disable_kerberos_support"></span><span id="DISABLE_KERBEROS_SUPPORT"></span>禁用 Kerberos 支持


连接到 IIS 时，SymSrv.dll 不支持 Kerberos 身份验证。 在这种情况下，必须在 IIS 和 NTLM 需要将其设置为唯一的 Windows 身份验证协议中禁用 Kerberos 身份验证。

**请注意**  仅在适用于你的环境时禁用 Kerberos 安全性。

 

**禁用使用 appcmd.exe 的 Kerberos 支持**

1.  打开命令提示符窗口

2.  若要禁用 Kerberos 和强制使用 NTLM，使用以下命令：

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='NTLM']" /commit:apphost
    ```

3.  若要启用了 Kerberos 返回默认值，请使用以下命令：

    ```console
    appcmd.exe set config -section:system.webServer/security/authentication/windowsAuthentication /+"providers.[value='Negotiate,NTLM']" /commit:apphost
    ```

## <a name="span-idconfiguringsymsrvclientauthenticationpromptsspanspan-idconfiguringsymsrvclientauthenticationpromptsspanspan-idconfiguringsymsrvclientauthenticationpromptsspanconfiguring-symsrv-client-authentication-prompts"></a><span id="Configuring_SymSrv_Client_Authentication_Prompts"></span><span id="configuring_symsrv_client_authentication_prompts"></span><span id="CONFIGURING_SYMSRV_CLIENT_AUTHENTICATION_PROMPTS"></span>配置 SymSrv 客户端身份验证提示


当 SymSrv 收到身份验证请求时，调试器可以显示身份验证对话框中，也可以自动拒绝该请求，具体取决于配置的方式。 可以配置此行为使用 ！ 上的符号提示 | 关闭。 若要开启提示，请使用此命令的示例。

```dbgcmd
!sym prompts on
```

若要检查的当前设置，请使用此命令。

```dbgcmd
!sym prompts
```

有关详细信息请参阅[ **！ 符号**](-sym.md)并[防火墙和代理服务器](firewalls-and-proxy-servers.md)。

 

 





