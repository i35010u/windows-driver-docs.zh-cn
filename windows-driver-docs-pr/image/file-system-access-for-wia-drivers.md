---
title: WIA 驱动程序的文件系统访问权限
description: WIA 驱动程序的文件系统访问权限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ce446842e4ea0f7082c74beb3bcb96129490e7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827999"
---
# <a name="file-system-access-for-wia-drivers"></a>WIA 驱动程序的文件系统访问权限





如果驱动程序需要使用的文件不是 WIA 服务在文件传输过程中提供的文件，则驱动程序必须小心地了解这些文件的位置以及如何访问这些文件。 具体而言，驱动程序编写人员应该知道它们所使用的目录和文件的访问权限。 驱动程序可能需要读取或写入自己的文件的一些示例包括日志记录、校准和保存配置。

例如，%*windir* % \\ *System32* 目录对于 **LocalService** 帐户是只读的，因此 WIA 驱动程序通常无法打开文件以进行读写访问。 大多数目录对于 **LocalService** 帐户都是只读的，因此，如果驱动程序只需读取文件，就很少会出现问题。 但是，当驱动程序尝试在受限目录中创建或写入文件时，会发生文件问题。

用于写入只有驱动程序使用的文件的安全位置位于用户配置文件目录中。 请注意，在这种情况下，用户是指在其下运行承载驱动程序的进程的帐户。 在 Windows XP 中，这是 **LocalSystem** 帐户，在 Microsoft Windows Server 2003 及更高版本中，是 **LocalService** 帐户。 为了使驱动程序在所有支持 WIA 的 Windows 版本中正常工作，驱动程序应在 userprofile 目录中创建其专用文件 **%** <em>userprofile</em> **%** 。

下面的代码示例演示 WIA 驱动程序如何使用%*userprofile*% 目录。

```cpp
#define MY_DRIVER_FILE_NAME_W L"%userprofile%\\MyDriverFile.ext";
HANDLE hMyDriverFile         = INVALID_HANDLE_VALUE;
WCHAR  wszFileName[MAX_PATH] = {L'\0'};
DWORD  dwMaxChars            = sizeof(wszExpandedName) /                     
                               sizeof(wszExpandedName[0]);
if (ExpandEnvironmentStringsW(MY_DRIVER_FILE_NAME_W, 
                              wszFileName,
                              dwMaxChars))
{
    //
    // The %userprofile% environment variable is expanded, if
    // there was an error and the variable is not found.
    // In this case an error would be returned before creating the 
    // file. If the file is created blindly with the name 
    // L"%userprofile\\MyDriverFile.ext"
    // a possibility exists that the file will be created in a 
    // different directory, e.g. the root.
    //
    hMyDriverFile = 
            CreateFileW(
            wszFileName,           // Contains file name and path
            dwDesiredAccess,       // E.g. GENERIC_WRITE
            dwShareMode,           // E.g. FILE_SHARE_WRITE
            lpSecurityAttributes,  // Don't forget to ACL your file            
                                   //   appropriately!
            dwCreationDisposition, // E.g. CREATE_ALWAYS
            dwFlagsAndAttributes,  // E.g. FILE_ATTRIBUTE_NORMAL
            NULL);                 // Template file
    if (hMyDriverFile != INVALID_HANDLE_VALUE)
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
```

如果驱动程序需要写入包含在 userprofile% 之外的目录中的文件 **%** <em>userprofile</em>，则应确保已为文件/目录设置了正确的权限。 通常，这意味着确保已向 **LocalService** 帐户授予适当的权限。 在 Windows XP 上，WIA 服务在属于本地管理员组并且具有相当高的访问级别的 **LocalSystem** 帐户下运行。

### <a name="wia-application-and-wia-driver-common-files"></a>WIA 应用程序和 WIA 驱动程序公用文件

如果驱动程序和捆绑的应用程序都需要对公共文件的读/写访问权限，则建议将该文件放入 "所有用户" 配置文件中的应用程序数据目录的子目录中， (CSIDL \_ common \_ APPDATA) 。 请确保在新子目录上设置相应的 Acl。

 

 




