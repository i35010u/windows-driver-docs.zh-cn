---
title: WIA 驱动程序的文件系统访问权限
description: WIA 驱动程序的文件系统访问权限
ms.assetid: 7bdd116e-d58f-4c2e-a5ec-c9a8196cfd62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa59a3155f22784ff36607c8c5715ca041e50bd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323443"
---
# <a name="file-system-access-for-wia-drivers"></a>WIA 驱动程序的文件系统访问权限





如果驱动程序需要使用文件传输过程中提供的 WIA 服务以外的文件，该驱动程序必须小心对待这些文件的位置和访问方式。 具体而言，驱动程序编写人员应知道的目录和文件，它们将使用的访问权限。 一些示例的读取或写入其自己的文件包括日志记录，校准，可能需要的驱动程序并保存配置。

例如，在 %*windir*%\\*System32*目录是只读的**LocalService**帐户，因此 WIA 驱动程序通常不能打开用于读取或写入访问权限的文件。 大多数目录是只读的**LocalService**帐户，因此有很少问题如果驱动程序只需从文件中读取。 但是，驱动程序尝试创建或受限制的目录中写入文件时，会出现文件问题。

安全的位置来编写驱动程序仅使用的文件是在用户配置文件目录中。 请注意，用户在这种情况下指运行承载该驱动程序的进程的帐户。 在 Windows XP 中，这是**LocalSystem**帐户，并在 Microsoft Windows Server 2003 和更高版本，它是**LocalService**帐户。 为了使驱动程序中正常运行的所有版本的 Windows 支持 WIA，驱动程序应创建及其专用文件置于**%** <em>userprofile</em> **%** 目录。

下面的代码示例演示如何 WIA 驱动程序可以使用 %*userprofile*%目录。

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

如果驱动程序需要写入文件的目录中而不包含**%** <em>userprofile</em>%，应确保已为文件/目录设置的正确权限。 通常，这意味着确保授予适当的权限**LocalService**帐户。 在 Windows XP 上 WIA 服务在运行下**LocalSystem**帐户，这属于本地管理员组并且具有高很多访问级别。

### <a name="wia-application-and-wia-driver-common-files"></a>WIA 应用程序和 WIA 驱动程序的常见文件

如果该驱动程序和捆绑应用程序需要读/写访问的常见文件，则建议将文件放入应用程序数据目录的子目录中的所有用户配置文件 (CSIDL\_常见\_APPDATA)。 请确保在新的子目录上设置适当的 Acl。

 

 




