---
title: 设置 Web 站点
description: 设置 Web 站点
ms.assetid: 9c719557-bca0-4c9c-9208-70e106d976f9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b31665742900d479fcd90231c7d4056a6ff9cd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555613"
---
# <a name="setting-up-the-web-site"></a>设置 Web 站点


设置从其共享的源文件，并记下站点的根目录下的网站。 您的源是然后可从站点如：

```text
https://SrcMachineName/source
```

为使源代码文件通过 Internet 访问，必须配置包含的源文件的目录。

选择索引的源所在的目录开始。 在示例中，我们调用此目录 c:\\源和在网络上的服务器的名称\\SrcMachineName。 必须设置权限，以便用户可以访问该站点，并且必须添加必须通过网络访问的源内容的安全组。 若要启用的安全会有所不同环境环境。 对于某些安装时，此组是**每个人都**。

**若要设置目录的权限：**

1.  打开**Windows 资源管理器**。

2.  展开**我的计算机**。

3.  展开 c： 驱动器。

4.  右键单击**c:\\源**，然后选择**共享和安全**。

5.  检查**共享此文件夹**按钮。

6.  单击**权限**按钮。

7.  验证所需的安全组添加下具有读取访问权限**组或用户名**和检查相应的框。

8.  单击**确定**退出的权限。

9.  单击**确定**退出源属性。

源目录现在可用于调试由另一台计算机使用的源路径为 srv\*\\\\SrcMachineName\\源。

 

 





