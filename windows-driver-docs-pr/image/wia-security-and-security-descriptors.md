---
title: WIA 安全和安全描述符
description: WIA 安全和安全描述符
ms.assetid: 2919f3fc-1eb5-4801-a589-ae3000320763
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 010e7f0231a43ba1249a4a4fc829b858c76e219a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352713"
---
# <a name="wia-security-and-security-descriptors"></a>WIA 安全和安全描述符





中列出的问题的解决方案的许多[WIA 安全性的常见问题](common-wia-security-problems.md)要求以具有如授予访问权限的相应实体的安全描述符对象**LocalService**帐户。

通常情况下， **LocalService**帐户有权访问其 Acl 允许的访问的资源**LocalService**帐户、 Everyone，或身份验证的用户。 该服务不能与其他应用程序，共享对象 （管道、 文件映射、 同步和等等），除非它将创建允许用户或组对对象的用户访问的任意访问控制 list(DACL)。

下面的代码示例说明了如何设置安全描述符。 如果应用程序和驱动程序需要共享的已命名的事件对象，可以使用此方法。

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

注册表项还使用适当的 Acl 创建通过 INF 文件。 例如，若要在只能访问管理员和下运行的驱动程序软件项中创建注册表项**LocalService**，将以下条目添加到您的 INF 文件：

```INF
[DDInstallSection]
Addreg=MyAddReg

[DDInstallSection.MyAddReg]
HKLM,"SOFTWARE\MyCompany\MySpecialKey\"

[DDInstallSection.MyAddReg.Security]
"D:(A;CIOI;GA;;;BA)(A;CIOI;GA;;;LS)"
```

有关 INF 文件的详细信息，请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)。

请参阅有关 Windows 安全模型的详细信息的 Windows 安全文档。 驱动程序编写人员还应了解的常规安全最佳做法，降低破坏性用户在成功地利用了其驱动程序中的漏洞的可能性。 "*Writing Secure Code*"(ISBN 0 7356 1588年 8) 的 Microsoft Press 是几个有用的资源可用。

 

 




