---
title: 安装驱动程序和示例应用
description: 本部分提供有关安装驱动程序和 WSD 示例应用程序的信息。
ms.assetid: BF89F0D0-2ED3-4900-996F-BB7B9C8C9B80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68294935d0f139e4faeecd5559c7e23e475b41a8
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652777"
---
# <a name="install-the-driver-and-sample-app"></a>安装驱动程序和示例应用


本部分提供有关安装驱动程序和 WSD 示例应用程序的信息。

## <a name="install-the-driver-on-a-windows81-machine"></a>在 Windows 8.1 计算机上安装驱动程序


若要安装3D 打印 SDK 中包含的打印驱动程序，请选择驱动程序的 .inf 文件，右键单击该文件，然后选择 "**安装**"。

## <a name="install-the-sample-app"></a>安装示例应用程序


首先安装 Microsoft Visual Studio 2013 （专业版或旗舰版），并应用所需的任何 service pack 或更新。

该示例实现包含在 ASP.NET 中实现的 Microsoft Internet Information Services （IIS） web 服务，其中包含一个响应 WS 打印协议请求的 http 处理程序。

定向发现可在运行 web 服务的情况下运行，因为它在不使用 UDP 发现的情况下使用 http 协议。

### <a name="installation-requirements"></a>安装要求

在 windows 计算机上部署 web 服务要求计算机与 Microsoft .NET 4.5 一起安装 IIS 和 ASP.NET。

### <a name="install-iis"></a>安装 IIS

1.  若要安装 IIS，请按**Windows** + **R**键组合以显示 "**运行**" 对话框，然后键入 `appwiz.cpl` 并按 " **enter**"。

    ![运行](images/wsd-app-1.png)

    这将打开 "控制面板" "**程序和功能**"。

2.  在**控制面板主页**窗格上，单击 **"打开或关闭 Windows 功能**"。

    ![程序和功能](images/wsd-app-2.png)

3.  在 " **Windows 功能**" 对话框中，选中 " **Internet Information Services** " 复选框。

    ![Windows 功能](images/wsd-app-3.png)

4.  展开 " **Internet Information Services** " 复选框，然后展开 "**万维网服务**"。

    ![world wide web 服务](images/wsd-app-4.png)

5.  展开 "**应用程序开发功能**"，并选择和子功能，如下所示：

    ![应用程序开发功能](images/wsd-app-5.png)

6.  单击**确定**。 "**应用更改**" 对话框将显示安装进度。

    ![应用更改](images/wsd-app-6.png)

7.  当 "**应用更改**" 对话框关闭时，打开浏览器并导航到 https://localhost 。

    ![localhost](images/wsd-app-7.png)

### <a name="publish-the-project"></a>发布项目

将处理程序项目发布到 localhost 以部署 web 服务。

![发布 web](images/wsd-app-8.png)

成功发布后，浏览到 https://localhost 会导致向后发送空文件。 如果未正确设置处理程序，您将收到一条错误消息，或者可能会看到默认的 IIS 网页。

可以切换**DefaultAppPool**以使用**NetworkService**标识运行，并且它将继续按预期方式工作。 **DefaultAppPool**还应在网络上同时工作。

### <a name="verify-site-bindings"></a>验证站点绑定

如果需要支持 IPv6，请确保为 IPv6 创建 ASP.NET 站点绑定。

处理程序项目将项目发布到**默认**网站。

默认情况下，站点绑定到所有 IP 地址上的端口80。

![网站绑定](images/wsd-app-9.png)

### <a name="update-windows-firewall"></a>更新 Windows 防火墙

默认情况下，Windows 会阻止计算机上的端口80，因此你需要更新 Windows 防火墙以允许万维网服务（http）入站流量入站。 如果不启用此启用，来自客户端的传入 http 请求将会失败。

![windows 防火墙](images/wsd-app-10.png)

### <a name="install-the-fabrikam-printer"></a>安装 Fabrikam 打印机

### <a name="directed-discovery-via-http-endpoint"></a>通过 Http 终结点的定向发现

1.  在控制面板中打开 "**设备和打印机** **"** 。

2.  选择 "**添加打印机**"。

3.  选择**未列出所需的打印机**。

    ![添加打印机](images/wsd-app-11.png)

4.  选择 "**使用 tcp/ip 地址或主机名添加打印机**"。

    ![通过其他选项查找打印机](images/wsd-app-12.png)

5.  从 "**设备类型**" 列表中选择 " **Web 服务设备**"。

    ![选择设备类型](images/wsd-app-13.png)

6.  键入主机名或 IP 地址，然后单击 "**下一步**"。

    将显示 "正在与**打印机联系 ...** " 进度栏。

    ![输入主机名或 ip 地址](images/wsd-app-14.png)

    安装 Fabrikam 打印机后，将显示以下消息：

    ![已安装 fabrikam 3d 打印机](images/wsd-app-15.png)

### <a name="ad-hoc-discovery-via-udp-multicast"></a>通过 UDP 多播的即席发现

可以通过实现侦听端口3702上的发现事件的 UDP 服务器来执行即席发现。

有关 exchange 序列的详细信息，请参阅[发现和元数据交换消息模式](https://docs.microsoft.com/windows/desktop/WsdApi/discovery-and-metadata-exchange-message-patterns)。

 

 




