---
title: WIA 安全和安全描述符
description: WIA 安全和安全描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95631bbcd0c0de1f62ea9646c0a9783ae6421b20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826415"
---
# <a name="wia-security-and-security-descriptors"></a>WIA 安全和安全描述符





[常见 WIA 安全问题](common-wia-security-problems.md)中列出的问题的许多解决方案都要求有问题的对象具有安全描述符，以便向适当的实体（如 **LocalService** 帐户）授予访问权限。

通常， **LocalService** 帐户有权访问其 Acl 允许 **LocalService** 帐户、Everyone 或经过身份验证的用户访问的资源。 该服务不能与其他应用程序共享 (管道、文件映射、同步等) 的对象，除非它创建一个随机访问控制列表 (DACL) 允许用户或用户组访问该对象。

下面的代码示例演示如何设置安全描述符。 如果应用程序和驱动程序需要共享一个已命名的事件对象，则可以使用此方法。

```cpp
//
//  Security descriptor in SDDL form:
//  D:           - Indicates what follows is a 
//                 Discretionary Access Control List (DACL)
//  (A;;GA;;;LS) - Grants generic all access to LocalService
//  (A;;GA;;;BA) - Grants generic all access to Built-in Admins
//  (A;;GA;;;IU) - Grants generic all access to Interactive User 
//
#define MY_EVENT_DACL TEXT("D:(A;;GA;;;LS)(A;;GA;;;BA)(A;;GA;;;IU)")

//
//  Allocate appropriate security attributes for the named event
//  to be shared between driver and app running under 
//  interactive user's account.
//
SECURITY_ATTRIBUTES sa = { sizeof(sa), FALSE, NULL };
if(ConvertStringSecurityDescriptorToSecurityDescriptor(
              MY_EVENT_DACL,
              SDDL_REVISION_1, 
              &(sa.lpSecurityDescriptor), NULL))
{
  h_MyEvent = CreateEvent(&sa,           // Our security descriptor 
                                         //  allowing access to 
                                         //  Admins, LocalService
                                         //  and the Interactive
                                         //  User
                          bManualReset,
                          bInitialState, 
                          tszName);
  if (h_MyEvent != NULL)
  {
      //  Success!
  }
  else
  {
      // Failed.  Do error cleanup...
      .
      .
      .
  }
}
else
{
  // Failed.  Do error cleanup...
  .
  .
  .
}
```

还可以通过 INF 文件使用相应的 Acl 创建注册表项。 例如，若要在软件密钥中创建仅供管理员使用的注册表项和在 **LocalService** 下运行的驱动程序，请将以下项添加到 INF 文件中：

```INF
[DDInstallSection]
Addreg=MyAddReg

[DDInstallSection.MyAddReg]
HKLM,"SOFTWARE\MyCompany\MySpecialKey\"

[DDInstallSection.MyAddReg.Security]
"D:(A;CIOI;GA;;;BA)(A;CIOI;GA;;;LS)"
```

有关 INF 文件的详细信息，请参阅 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md)。

有关 Windows 安全模型的详细信息，请参阅 Windows 安全文档。 驱动程序编写人员还应了解常见的安全最佳做法，从而减少破坏性用户成功利用其驱动程序中的漏洞的可能性。 "*编写安全代码*" (Microsoft 按下的 ISBN 0-7356-1588-8) 是可用的几个有用资源之一。

 

 




