---
title: 安装驱动程序和示例应用
description: 本部分提供安装该驱动程序和 WSD 示例应用程序的信息。
ms.assetid: BF89F0D0-2ED3-4900-996F-BB7B9C8C9B80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36f5f9d432dc584864a1a6efb29c924fcf24382
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519508"
---
# <a name="install-the-driver-and-sample-app"></a>安装驱动程序和示例应用


本部分提供安装该驱动程序和 WSD 示例应用程序的信息。

## <a name="install-the-driver-on-a-windows81-machine"></a>在 Windows 8.1 计算机上安装驱动程序


要安装 3D 打印 SDK，并选择在驱动程序.inf 文件中包含的打印驱动程序，请右键单击该文件，然后选择**安装**。

## <a name="install-the-sample-app"></a>安装示例应用


首先安装 Microsoft Visual Studio 2013 （专业版或旗舰版） 和应用任何需要 service pack 或更新。

该示例实现包含在 ASP.NET 中实现与 WS 打印协议请求响应的 http 处理程序的 Microsoft Internet 信息服务 (IIS) web 服务。

定向的发现可以运行与 web 服务正在运行，因为它起作用，而无需 UDP 发现的 http 协议关闭。

### <a name="installation-requirements"></a>安装要求

在 windows 计算机上的 web 服务的部署要求计算机具有以及 Microsoft.NET 4.5 安装 IIS 和 ASP.NET。

### <a name="install-iis"></a>安装 IIS

1.  若要安装 IIS，请按**Windows** + **R**组合键以打开**运行**对话框框中，然后键入`appwiz.cpl`按**Enter**.

    ![运行](images/wsd-app-1.png)

    这将打开控制面板**程序和功能**。

2.  上**控制面板主页**窗格中，单击**打开或关闭打开的 Windows 功能**。

    ![程序和功能](images/wsd-app-2.png)

3.  在中**Windows 功能**对话框中，选择**Internet Information Services**复选框。

    ![windows 功能](images/wsd-app-3.png)

4.  展开**Internet 信息服务**复选框，然后展开**World Wide Web 服务**。

    ![world wide web 服务](images/wsd-app-4.png)

5.  展开**应用程序开发功能**和 select 和子功能如下所示：

    ![应用程序开发功能](images/wsd-app-5.png)

6.  单击“确定” 。 **将更改应用**对话框将显示安装进度。

    ![应用更改](images/wsd-app-6.png)

7.  当**将更改应用**对话框关闭，打开浏览器并导航到 http://localhost。

    ![localhost](images/wsd-app-7.png)

### <a name="publish-the-project"></a>发布项目

处理程序项目发布到 localhost 来部署 web 服务。

![发布 web](images/wsd-app-8.png)

发布成功后，浏览到 http://localhost将导致发送回的空文件。 如果处理程序未正确设置，将收到一条错误消息，或可能会看到默认 IIS 网页。

您可以切换**DefaultAppPool**若要使用运行**NetworkService**标识和它将继续按预期方式工作。 **DefaultAppPool**应在整个还可以在网络。

### <a name="verify-site-bindings"></a>验证站点绑定

如果需要支持 IPv6，请确保为 IPv6 创建 ASP.NET 网站绑定。

处理程序项目发布到项目**Default Web Site**。

默认情况下，在站点绑定到端口 80 上的所有 IP 地址。

![站点绑定](images/wsd-app-9.png)

### <a name="update-windows-firewall"></a>更新 Windows 防火墙

默认情况下，Windows 块在计算机上的端口 80，因此将需要更新 Windows 防火墙以允许 World Wide Web 服务 (http) 流量入站。 无需打开这，从客户端的传入 http 请求将失败。

![windows firewall](images/wsd-app-10.png)

### <a name="install-the-fabrikam-printer"></a>安装 Fabrikam 打印机

### <a name="directed-discovery-via-http-endpoint"></a>通过 Http 终结点定向的发现

1.  打开**设备和打印机**中**控制面板**。

2.  选择**添加打印机**。

3.  选择**需的打印机未列出**。

    ![添加打印机](images/wsd-app-11.png)

4.  选择**使用 TCP/IP 地址或主机名添加打印机**。

    ![通过其他选项查找打印机](images/wsd-app-12.png)

5.  选择**Web 服务设备**从**设备类型**列表。

    ![选择设备类型](images/wsd-app-13.png)

6.  键入主机名或 IP 地址，然后单击**下一步**。

    **联系打印机...** 进度栏将显示。

    ![输入主机名或 ip 地址](images/wsd-app-14.png)

    Fabrikam 打印机安装时将显示以下消息：

    ![fabrikam 3d 打印机安装](images/wsd-app-15.png)

### <a name="ad-hoc-discovery-via-udp-multicast"></a>临时模式下通过 UDP 多播

可以通过实现端口 3702 上的发现事件进行侦听的 UDP 服务器执行临时发现。

有关 exchange 序列的详细信息，请参阅[发现和元数据交换消息模式](https://msdn.microsoft.com/library/windows/desktop/bb513677.aspx)。

 

 




