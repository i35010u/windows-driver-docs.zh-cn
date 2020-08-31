---
title: 避免在设备安装和驱动程序更新过程中重新启动
description: 在设备安装和驱动程序更新过程中避免系统重启
ms.assetid: b30c9e5f-85af-4e7f-81aa-67fe2df8a178
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddcfa9b6ebff67d213416c6eb94074aa8c9a6764
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095107"
---
# <a name="avoiding-system-restarts-during-device-installations-and-driver-updates"></a>在设备安装和驱动程序更新过程中避免系统重启


若要在设备安装过程中避免系统重启，请使用以下规则：

-   请勿在[**INF DDInstall 部分**](inf-ddinstall-section.md)中使用 "**重新启动**" 或 "**重新启动**" 条目。 这些指令最初是为与 Windows 9x/Me 兼容而提供的，不应用于 Windows 2000 和更高版本的 Windows。

-   除非绝对必要，否则不要使用 COPYFLG_FORCE_FILE_IN_USE 或使用 [**INF CopyFiles 指令**](inf-copyfiles-directive.md)COPYFLG_REPLACE_BOOT_FILE 标志。

-   为类安装程序或共同安装程序或服务 DLL 的每个新版本分配一个新的文件名。 如果使用的是较旧的版本，这就不必重新启动系统。  (事实上，如果新文件名不用于更新的类安装程序或类共同安装程序，则这些新文件将不用于安装。 ) 

-   若要更新设备的驱动程序，请遵循 " [更新驱动程序文件](updating-driver-files.md)" 下列出的规则。

## <a name="minimizing-restarts-when-updating-file-backed-drivers"></a>当更新文件支持的驱动程序时最小化重新启动


在 Windows 10 之前，所有内核模式驱动程序都是由系统的分页文件支持的。 因此，即使驱动程序正在运行，也可以在磁盘上覆盖驱动程序二进制文件。

为了提高性能，从 Windows 10 开始，大多数非启动启动驱动程序都是由磁盘上的驱动程序二进制文件提供支持。

现在支持文件的驱动程序启动类型包括：

-    (0x00000001) SERVICE_SYSTEM_START
-   SERVICE_AUTO_START (0x00000002) 
-   SERVICE_DEMAND_START (0x00000003) 

页面文件继续支持启动启动驱动程序。

若要更新文件备份的驱动程序，请使用下列最佳做法。 否则，更新可能需要两次重启，一个用于替换文件，另一个用于加载新版驱动程序。

如果使用的是 INF 文件，请执行以下步骤：

1.  修改驱动程序 INF 文件的 **CopyFiles** 部分以使用 **COPYFLG_IN_USE_RENAME**，如下所示：

    ```cpp
    [MyDriver_Install.NT]
    CopyFiles=MyDriverCopy
     
    [MyDriverCopy]
    MyDriver.sys,,,0x00004000  ; COPYFLG_IN_USE_RENAME
    ```

    如果使用此标志，则 Windows 将尝试替换磁盘上的驱动程序文件。 有关详细信息，请参阅 [INF CopyFiles 指令](inf-copyfiles-directive.md)。

2.  如果 INF 用于 PnP 驱动程序，则在设备安装期间，Windows 将尝试卸载正在运行的驱动程序并重新启动使用该驱动程序的设备，以便选取新版本的驱动程序。 如果此操作失败，则设备安装将指示系统应重新启动。
3.  如果 INF 不适用于 PnP 驱动程序，并且使用 [**InstallHInfSection**](/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona) 等方法来处理 inf，则手动停止并重新启动该驱动程序：
    -   关闭驱动程序的所有打开的句柄，然后使用以下内容之一停止驱动程序：

        -   **sc.exe 停止** * &lt; mydriver &gt; *
        -   **Control 服务 (SERVICE_CONTROL_STOP) **

        有关详细信息，请参阅 [**control 服务函数**](/windows/desktop/api/winsvc/nf-winsvc-controlservice)。

如果使用的不是 INF 文件，请使用以下步骤：

1.  如上文所述，停止该驱动程序。 将旧的驱动程序二进制文件替换为新的。
2.  如果无法停止驱动程序，请重命名现有文件，将新文件复制到该位置，并设置要在将来删除的现有文件 (例如，将 [**MoveFileEx**](/windows/desktop/api/winbase/nf-winbase-movefileexa) 与 **MOVEFILE_DELAY_UNTIL_REBOOT** 标志) 一起使用。 为了开始使用新版本的驱动程序，系统需要重新启动。

## <a name="related-topics"></a>相关主题


[基于文件和基于页文件的节](../kernel/file-backed-and-page-file-backed-sections.md)

[如何确定驱动程序的加载时间](../ifs/what-determines-when-a-driver-is-loaded.md)

 

