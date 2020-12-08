---
title: 设置网站
description: 设置网站
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b91d1dd675fd9d081d9d262adbfb103f77b8640
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836867"
---
# <a name="setting-up-the-web-site"></a>设置网站


设置一个网站，该网站用于共享源文件，而不是站点的根目录。 然后，可以从以下站点获取源：

```text
https://SrcMachineName/source
```

为了使源文件可通过 Internet 访问，您必须配置包含源文件的目录。

首先选择索引源所在的目录。 在我们的示例中，我们在网络 SrcMachineName 上调用此目录 c： \\ source 和服务器的 \\ 名称。 必须设置权限，以便用户可以访问站点，并且必须添加必须通过网络访问源内容的安全组。 要实现的安全数量因环境而异。 对于某些安装，此组是 **Everyone**。

**若要设置目录的权限，请执行以下操作：**

1.  打开 **Windows 资源管理器**。

2.  展开 **我的电脑**。

3.  展开 C：驱动器。

4.  右键单击 " **c： \\ 源** "，然后选择 " **共享和安全**"。

5.  选中 " **共享此文件夹** " 按钮。

6.  单击 " **权限** " 按钮。

7.  在 " **组或用户名** " 下面添加并选中相应的框，以验证所需的安全组是否具有 "读取" 访问权限。

8.  单击 **"确定"** 退出权限。

9.  单击 **"确定" 退出 "** 源属性"。

源目录现在可用于由源路径为 srv \* \\ \\ SrcMachineName 源的另一台计算机进行调试 \\ 。

 

 





